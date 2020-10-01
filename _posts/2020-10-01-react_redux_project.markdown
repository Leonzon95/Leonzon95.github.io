---
layout: post
title:      "React Redux Project"
date:       2020-10-01 18:51:08 +0000
permalink:  react_redux_project
---


For my react project I built an app called Cleans. This app helps people hire someone to hire their living space. It has two kind of users: one user can post jobs adn hire someone, the othe user can look at all of the available jobs and apply to them, which could potentially get them hired for the job. Since jobs have different statuses (new, pending, and completed) and the jobs that a the two kinds of users are going to see are completely different, I needed to write two filtering algorithm to separate the jobs into their own category. One of my challenges implementing these algorithms was: where is the best place to put these algorithms?

The first thing that came to mind is that I was going to put them in the reducer, but thinking about it a more, I realized that implementing these filtering algorithms in the reducer would make my reducer very messy and hard to read. So I made the choice that the best place to put it would be in the twodifferent containers that recived the `mapStateToProps`. Furthermore, they would actually be put in the  `mapStateToProps`, because that way the container is already recieving the filtered jobs and it can smoothly tell them to go where they have to. 

This is the function for the users that can post jobs:

```
const mapStateToProps = state => {
    const newJobs = [];
    const pendingJobs = [];
    const completedJobs = [];
    for (const job of state.jobs.data) {
        if (job.status === "new") newJobs.push(job);
        if (job.status === "pending") pendingJobs.push(job);
        if(job.status === "completed") completedJobs.push(job);
    }
    return {
        newJobs: newJobs,
        pendingJobs: pendingJobs,
        completedJobs: completedJobs,
        addresses: state.addresses.data,
        isAddressesLoading: state.addresses.loading,
        isJobsLoading: state.jobs.loading
    }
}
```

And this is for the other kind ofuser:

```
const mapStateToProps = state => {
    const user = state.user.user;
    const jobs = [];
    const appliedJobs = [];
    const pendingJobs = [];
    const completedJobs = [];
    for (const job of state.jobs.data) {
        if (job.hiredCleanerId === user.id) {
            if (job.status === "pending"){
                pendingJobs.push(job);
                continue;
            } else {
                completedJobs.push(job);
                continue;
            }
        } else if (job.status === "new"){
            let isAnApplicant = false;
            for (const applicant of job.applicants) {
                if (applicant.id === user.id) {
                    appliedJobs.push(job)
                    isAnApplicant = true;
                    break;
                }
            }
            if(!isAnApplicant) jobs.push(job);
        }
    }
    return {
        jobs: jobs,
        appliedJobs: appliedJobs,
        pendingJobs: pendingJobs,
        completedJobs: completedJobs,
        isJobsLoading: state.jobs.loading
    }
}
```

These two algorithms alone are pretty chunky and we're not even taking into consideration what kind of user we're filtering for, the container already knows. You can imgane that it would make the reducer function very messy.
