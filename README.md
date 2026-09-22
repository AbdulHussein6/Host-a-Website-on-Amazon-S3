<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Host a Website on Amazon S3

**Project Link:** [View Project](https://nextwork.ai/projects/70e2d059-31ab-5f67-8c58-f5edbd451140)

**Author:** Abdul Hussein  
**Email:** abdulhussein@hotmail.se

---

![Image](https://nextwork.ai/authentic_blue_lucky_ferret/uploads/70e2d059-31ab-5f67-8c58-f5edbd451140_5d4474f9)

## Introducing Today's Project!

### Project overview

In this project, I created an S3 bucket in Amazon S3, upload my website's files (HTML, CSS, and any other assets) to that bucket, and configure the bucket for static website hosting so the site is publicly accessible via an S3 website endpoint.

### Tools and concepts

Services I used were Amazon S3, primarily for object storage and static website hosting. Key concepts I learnt include how S3 buckets work as globally unique storage containers, how to configure public access and bucket policies to safely expose content to the internet, and how S3's static website hosting feature turns a simple storage bucket into a fully functional web server without needing a traditional backend.

### Time, challenges, and wins

This project took me approximately 30–45 minutes to complete. The most challenging part was configuring the bucket policy and public access settings correctly — getting the permissions right so the website would be publicly viewable without over-exposing the bucket took a bit of trial and error. It was most rewarding to see my website go live at the S3 endpoint URL — turning a plain storage bucket into a working, publicly accessible website felt like a great payoff for a fairly quick project.

## How I Set Up an S3 Bucket

### What I did in this step

Navigating to Amazon S3 in the AWS Console, then creating a bucket to act as the storage space for my website files.

### How long it took to create the bucket

Creating an S3 bucket took me less than a minute.

### Region selection

I picked Europe (Stockholm) — eu-north-1, since that was the region automatically selected based on my location. I kept it since choosing a region close to me helps reduce latency for accessing the console and testing the site, and Stockholm's data centers also run on renewable energy, which is a nice bonus for a learning project.

### Understanding bucket name uniqueness

It means that no two S3 buckets in the world can share the same name — not just within my own AWS account, but across every AWS account globally. S3 bucket names form part of a DNS namespace (since buckets can be accessed via URLs like bucket-name.s3.amazonaws.com), so if someone else has already claimed a name like my-website, I can't use it too, even if we're in different regions or different AWS accounts entirely. That's why bucket names often need extra uniqueness added, like your username, a project name, or random numbers.

![Image](https://nextwork.ai/authentic_blue_lucky_ferret/uploads/70e2d059-31ab-5f67-8c58-f5edbd451140_ba6d42ad)

## Upload Website Files to S3

### What I did in this step

In this step, I download the HTML file and the zip file of images provided for the website, then upload both files into my S3 bucket, because these files make up the actual content of my website, and S3 needs them stored in the bucket before I can configure it to serve them as a live site.

### Files I uploaded

The two files I uploaded were an HTML file (which set up the structure and content of the website's homepage) and a zip file of images (which contained the image assets used throughout the site). I unzipped the image file and made sure both the HTML file and the extracted images were uploaded into my S3 bucket.

### How the files work together

My guess is that the HTML file is the actual webpage structure/content — the text, layout, and code — while the zip file contains the images that the HTML file references (like a logo, banner, or background images) using <img> tags or CSS. The HTML file needs the image files to be present in the bucket so that when the page loads in a browser, it can pull in and display those images alongside the text. Without the images uploaded too, the page would load but show broken image icons where those pictures should appear.

![Image](https://nextwork.ai/authentic_blue_lucky_ferret/uploads/70e2d059-31ab-5f67-8c58-f5edbd451140_a265af88)

## Static Website Hosting on S3

### What I did in this step

In this step, I enabled static website hosting on my S3 bucket and specify the index document (and error document) for the site, because this setting turns the bucket from a plain file storage container into an actual web server that can serve my HTML page directly through a public S3 website endpoint URL. Once enabled, I'll visit that public link to confirm my website is live.

### Understanding website hosting

Website hosting means that instead of just storing files privately, my S3 bucket is configured to serve those files over HTTP as a website, accessible to anyone via a public URL — so visitors can open their browser, go to that link, and view my site just like they would any other website on the internet.

### How I enabled website hosting

To enable website hosting with my S3 bucket, I went to the Properties tab of my bucket, scrolled down to Static website hosting, clicked Edit, selected Enable, chose "Host a static website" as the hosting type, entered index.html as the index document, then saved the changes. This gave me a public S3 website endpoint URL that I could visit to view my live site.

### Access Control Lists (ACLs)

An Access Control List (ACL) is a legacy access-management mechanism in S3 that lets you grant basic read/write permissions to specific AWS accounts or predefined groups (like "everyone") at the individual object or bucket level. It's a more granular but older and less flexible tool compared to bucket policies and IAM, and AWS now recommends using bucket policies instead for most use cases.

I actually enabled ACLs at first, just to test out how they worked and see the permission options they offered. After experimenting with them, I switched to using a bucket policy instead to manage public access to my website files, since that's the more modern and centralized approach AWS recommends for controlling access at the bucket level.

![Image](https://nextwork.ai/authentic_blue_lucky_ferret/uploads/70e2d059-31ab-5f67-8c58-f5edbd451140_c22c54c0)

## Bucket Endpoints

### Understanding bucket endpoint URLs

Once static website hosting is enabled, S3 produces a bucket endpoint URL, which is the public web address you can use to access your website directly through a browser.

### What I saw when I tested the endpoint

When I first visited the bucket endpoint URL, I saw a 403 Forbidden error. The reason for this was that my bucket didn't yet have public read permissions set up — even though I'd enabled static website hosting and unblocked public access settings.

![Image](https://nextwork.ai/authentic_blue_lucky_ferret/uploads/70e2d059-31ab-5f67-8c58-f5edbd451140_22ce4daf)

## Success!

### What I did in this step

In this step, I set the ACL on my website files to allow public read access, because without it, visitors get a 403 Forbidden error trying to view the site.

### How I resolved the 403 error

To resolve this 403 Forbidden error, I uploaded the unzipped folder and did a re-set on the ACLs and then clicked the link again.

![Image](https://nextwork.ai/authentic_blue_lucky_ferret/uploads/70e2d059-31ab-5f67-8c58-f5edbd451140_5d4474f9)

## Bucket Policies

### What I did in this extension

In this project extension I implemented a bucket policy that denies deleting any objects in the bucket. I'm doing this so that I also understand why bucket policies are important — unlike ACLs, which only grant permissions.

### Understanding bucket policies

An alternative to ACLs are bucket policies, which are rules written in JSON that you attach to the whole bucket to control who can access it and what they're allowed to do (like read, upload, or delete files). The benefit of using bucket policies is that they're more powerful and flexible — you can set detailed rules for the entire bucket in one place, including explicitly blocking certain actions, which makes it easier to manage permissions as your project grows — while ACLs are useful for simple, quick access control on individual files, like just making one object public, without needing to write a full policy.

![Image](https://nextwork.ai/authentic_blue_lucky_ferret/uploads/70e2d059-31ab-5f67-8c58-f5edbd451140_sm2sm2sm)

### What my bucket policy does

My bucket policy denies the delete action for everyone, including the public, on my website files. I tested this by trying to delete one of my objects in the S3 console after applying the policy, and saw that the delete action failed with an "Access Denied" error, confirming that the policy successfully blocked deletion even though the files remained publicly readable.

---

*Built with [NextWork](https://nextwork.ai) - [View this project](https://nextwork.ai/projects/70e2d059-31ab-5f67-8c58-f5edbd451140)*
