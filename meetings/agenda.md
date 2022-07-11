# Next Technical Steering Committee Meeting Agenda

- Date: 2022-07-11
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### Future of the migration layer

We should think about how to proceed with `laminas/laminas-dependency-plugin` and `laminas/laminas-zendframework-bridge`.
Due to the latest issues reported in the zendframework bridge (https://github.com/laminas/laminas-zendframework-bridge/issues/95 https://github.com/laminas/laminas-zendframework-bridge/pull/94) and the recent movement of composer not following semver anymore, archiving both `laminas/laminas-dependency-plugin` with `laminas/laminas-zendframework-bridge` might be considered as the best option.

Abandoning old migration stuff after 2,5 years might be okay.

So questions are: 
 - Should we abandon both packages? 
 - What components do still rely on the bridge?
 - Should we release a new version of these components relying on the bridge so they're not blocking upstream projects getting rid of the bridge?

### Possibilities for project backers

In the early TSC-meetings the funding of the project as well as possibilities for backers were discussed. A thing I remember, but cannot find in the minutes, was some idea project backers to be listed in some form on the website. Maybe it was in connection with a list of "official" agencies providing support.

The topic has not been discussed recently. I would like to know if there are any news on this? 
