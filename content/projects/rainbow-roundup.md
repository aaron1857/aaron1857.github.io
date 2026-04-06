+++  
title = 'Rainbow Roundup'  
date = 2026-04-06T08:56:07-05:00  
authors = ["Aaron"]
banner = "img/ETC_Rainbow-Roundup_Logo.png"
draft = false
+++

# UTDesign EPICS Project

## What is this?

I took part in a project with UTDesign EPICS, which is a program in UTD that allows students to work with a team of other students to help a nonprofit organization with an issue they are having. This problem could simply be, “Our organization manages its data through an Excel spreadsheet, and we would like a nice interface with an actual database to manage it instead.” Though it can be something much more complex, as was the case for Rainbow Roundup. These projects are often multi-semester-long projects that can go on for multiple years and are inherited by a different team each semester.

Our project partner, Rainbow Roundup, wanted a web app to manage all the events they organize for the local LGBTQ+ community. They additionally wanted this web app to be able to sell their merchandise, which our partner had to previously coordinate manually.

## What did I actually work on?

I, personally, worked on refining the signup process, such as allowing a user to specify any family they are bringing along. Additionally, I was also responsible for the complete migration of our authentication system from Nuxt Auth to Better Auth. We had numerous issues with Nuxt Auth, including a deal-breaking bug where a user could not actually log in to an iOS PWA. Another big feature I implemented was adding native device notifications through the Web Push API. Which would allow the web app to send direct on-device notifications if the user chooses to opt into them. I also did many other smaller things and had a pretty fun time learning web development as well as how to actually make and deploy a web app (yes, I actually got to help with the deployment of the web app to AWS!).

#### That sounds awesome! Can I see it?

Sure! Go to <https://rainbow-roundup.npts.tech>, the project is currently deployed there.