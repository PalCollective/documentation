```mermaid
gantt
    title MVP Launch Strategy
    %% This gantt chart does use actual time units, instead, it
    %% recycles the "day" the part of dates to convey sequential
    %% steps as an arbitrary time unit. To advance this arbitrary
    %% time unit, use the "d" suffix (since the time units is tied
    %% to the "day" part of the the gantt dates).
    %% In this case, the year is irrelevant and can be set to any
    %% year in a two-digit format ("YY" below).
    dateFormat YY-DDD
    axisFormat Step %e
    section Development
        MVP-1 :ph11, 00-001, 1d
        MVP-2 :ph12, after ph11, 1d
        MVP-3 :ph13, after ph12, 1d
        MVP-4 :ph14, after ph13, 1d
        Milestone (MVP):milestone, mvp, after ph14, 0d
    section Communication
        Partner with Olive Branch Col :pa1, 00-001, 1d
        Invite Olive Branch Col staff to platform :after pa1, 2d
        Recruit team users: pa2, 00-001, 1d
        Verification training: pa3, after pa2, 1d
        Trained team members join platform: pa4, after pa3, 1d
```

- `MVP-1` features:
  - Public listing that can be viewed by anyone
  - Ability to create partner invites, by admins.
  - _Partner-verified_ end users[^3] (the only type of end users at this point), can post ads[^1] to the public listing
- `MVP-2` features:
  - Create a public _end user signup_, leading to the creation of `unverified` users
  - Unverified users can now post ads[^1] to the public listing, which shows next to their verifications
  - By the end of this step, we have `partner verified` and `unverified` ads in a public listing, mostly made of "GoFundMe campaign links".
- `MVP-3`:
  -  Ability to create _pals or team user[^2] invites_, by admins.
  -  Pals have real-time access to verification requests.
  -  Pals have real-time access to newly posted ads and requests, and have the ability to tag/approve them.
- `MVP-4` features:
  - End users can now request ID/Gaza verification.
  - Verification requests are logged with the IP of the requester. Pals see these requests popping up in real time.
  - Depending on the type of verification, we might transition to a secure chat to exchange and vet personal information, or request an anonymous video call (unsure how at this point).
  - Pals must be able to add verifications to end user profile data, including failed verifications.
- `MVP Milestone`:
  - A public listing of crowdfunding campaigns including ones made by users with different verifications.

[^3]: End users, or simply the users of our platform, are the ones making ads/requests and responding to requests, in an effort to share solidarity with others for Gaza.
[^1]: Ads are public listing items that do not accept responses and have no visibility filters (they can be seen by everyone, even those who are guests and not end users.
[^2]: Pals (previously team users) are, unlike end users, are users who are recruited by the platform to conduct human verifications and other team tasks. Their responsibilities may also change
over time, for example, they may tag requests initially, then transition to more of an approver after the tags become a part of the request form, as end users become more aware
and experienced, and our interface become more intuitive.
    
