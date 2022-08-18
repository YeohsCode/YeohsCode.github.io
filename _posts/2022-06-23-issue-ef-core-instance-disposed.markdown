---
layout: post
title:  EF core instance auto disposed issue
date:   2022-06-23 11:07:01 +0800
image:  17.jpg
tags:   Dev EF-Core Asp.Net C# Entity-Framework-core
---

I got a weird issue on EF core these days

I have a web API, it will start a async call to download docs and save data to db, the process is like:

	1. Check if there's existing Job
	2. If not, create a new Job in DB
	3. Download docs from Azure Storage account
	4. Convert Excel data to Biz models
	5. Save data to DB
	6. Update Job in DB to mark it as "Done"

The whole process was running in a async task without await.

The issue happens at the step 6 when querying the DB to get the running job by job Id, it says the Dbcontext instance has been disposed, however if we debug the code, the dbcontext is not null.

- Tried to override the Dispose method, it was not called.
- Tried to update the lifetime to optionsLifetime: ServiceLifetime.Transient in Startup, the instance was not regenerated.
- Tried to use AddAysnc instead of Add when add new job record in setup 2, not luck.

#### Solution 1:
Add IsDispose = false
Override Dispose() & DisposeAsync, set IsDispose = true;
When get the Dbcontext, check the IsDispose == true, if true, rebuild the instance

#### Solution 2:
USE HangeFire
使用 BackgroundJob.Enqueue(() => public method()); 这种方式 外层的 Dbcontext 依然会被 dispose, 但是通过 debug 可以发现在里面调用时似乎又自动生成了新的对象，问题得以解决。

~~似乎和Hangfire 无关，当我把 step 3-6 的代码从 controller 层移到 service层后，无论用哪种方式，总会自动生成新的 Dbcontext instance…~~

Double check 了一下，经 debug 证实 Hangfire 在跑 BackgroundJob.Enqueue 时 Dbcontext instance 也被 dispose，但是二次调用时会自动生成新的 instance。