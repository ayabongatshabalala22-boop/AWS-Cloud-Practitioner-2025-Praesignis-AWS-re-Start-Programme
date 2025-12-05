@MALLS - Africa's Finest Roots
A Group Project: Moving a Traditional South African Restaurant Online with AWS
This was a group AWS-re-Star-programme-project on November 2025 Cohort with Praesignis, where five of us built a modern, low-cost online presence for a fictional (but very realistic) South African restaurant – @MALLS. We took a real-world problem many small restaurants still face in 2025 (paper bookings, WhatsApp orders, no customer database) and fixed it using a static website on AWS S3 with a bunch of serverless services for the dynamic parts.

Live site: Our static website

The Team
We worked together and each had our own focus area:

Mokgadi M. – Web Development
Skhumbuzo S. – Web Development
Aytee A. – Research & Documentation
Lethabo L. – AWS S3 Deployment + Infrastructure
Leah L. – Presentation & Design
Proudly South African – hence all the orange and the flag vibes :)

The Problem (Real Restaurant Struggles)
Before we touched anything, the restaurant was running completely manually:

Order mix-ups and wrong dishes all the time
Double-bookings → angry customers waiting for tables
No central customer database → repeat customers treated like strangers
Staff shortages making everything worse
They were spending over R6 000 a month just on phone bills, printed menus, and lost business.

Our Solution
A fast, good-looking static website hosted on AWS S3 with these features:

Gallery of delicious dishes
Dine-in reservation form
Take-away / delivery order form
Simple loyalty program (earn points, redeem meals)
User registration & login
Interactive map with directions
Contact info and opening hours
Even though the front-end is static, everything that needs to be dynamic (forms, logins, storing bookings/orders) is handled by serverless AWS services – no servers to manage!

Tech Stack / AWS Services We Used
Service	What it does
S3	Hosts the static website and all images
CloudFront	CDN – makes the site load crazy fast worldwide
Route 53	DNS and our custom domain
Certificate Manager	Free SSL (https)
API Gateway	Receives form submissions
Lambda	Backend logic for bookings, orders, loyalty
DynamoDB	Stores reservations, orders, loyalty points
Cognito	User sign-up / sign-in
Amazon Location Service	Interactive map on the contact page
Cost – This Blew Our Minds
After everything was live, the total monthly AWS bill came to R540 – R630.
Compared to the old manual system that was indirectly costing them +R6 000/month, that’s a no-brainer.

Breakdown (approximate):

CloudFront: ~R470 (the biggest chunk)
DynamoDB: ~R48
Route 53: R16
Lambda, API Gateway, S3: just a couple of rands each
Cognito, ACM, Location Service: Free tier
What We Learned
You can build a fully functional “dynamic” site without ever touching a traditional server
Serverless is insanely cheap for small-to-medium traffic
Deploying updates takes minutes, not days
Security, backups, and scaling are basically handled for you
Small businesses in SA can compete with the big guys if they move to the cloud
How to Run Locally
If you clone this repo and just want to see the front-end:

# open index.html in your browser – that’s literally it
# or use a local server if you prefer
npx serve .
The backend (Lambda functions, API Gateway, etc.) is not in this repo because we deployed it separately via the AWS console / SAM for the project demo.

Final Thoughts
This project started as a simple “deploy a static site to S3” assignment and ended up becoming a full cloud migration case study. We’re really proud of what the five of us managed to pull together in a short time, and honestly, any real restaurant could copy this setup tomorrow and save thousands every month.

Feel free to fork, steal ideas, or hit us up if you want help doing something similar for your own business!

Made with ☕ braai vibes and a lot of late nights in November 2025
