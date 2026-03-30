# 🚀 Deploy Your Portfolio to AWS S3

Your portfolio website is ready! Here's a complete step-by-step guide to deploy it to AWS S3 and get it live on the internet.

---

## **Prerequisites**
- AWS Account (with free tier available)
- AWS CLI installed on your computer
- Your two HTML files: `index.html` and `projects.html`

---

## **Step 1: Create an S3 Bucket**

### **Via AWS Console (Easiest)**

1. Go to [AWS S3 Console](https://s3.console.aws.amazon.com/s3/home)
2. Click **Create bucket**
3. **Bucket name:** `dhanush-portfolio` (must be globally unique, so use something like `dhanush-portfolio-2024`)
4. **Region:** Select closest to you (e.g., `ap-south-1` for India)
5. **Block Public Access:** Leave as default (we'll configure access later)
6. Click **Create bucket** ✅

### **Via AWS CLI**
```bash
aws s3 mb s3://dhanush-portfolio-2024 --region ap-south-1
```

---

## **Step 2: Upload Your HTML Files**

### **Via AWS Console**

1. Open your newly created bucket
2. Click **Upload**
3. Drag and drop both files:
   - `index.html`
   - `projects.html`
4. Click **Upload** ✅

### **Via AWS CLI**
```bash
aws s3 cp index.html s3://dhanush-portfolio-2024/
aws s3 cp projects.html s3://dhanush-portfolio-2024/
```

---

## **Step 3: Enable Static Website Hosting**

1. Open your bucket in AWS Console
2. Go to **Properties** tab (bottom of page)
3. Scroll to **Static website hosting**
4. Click **Edit**
5. Enable **Static website hosting** ✅
6. **Index document:** `index.html`
7. **Error document:** `index.html` (for clean 404 handling)
8. Click **Save changes**
9. Copy your **Bucket website endpoint** (looks like: `http://dhanush-portfolio-2024.s3-website-ap-south-1.amazonaws.com`)

---

## **Step 4: Configure Bucket Policy for Public Access**

Your website needs to be publicly accessible.

1. Go to **Permissions** tab
2. Click **Bucket policy**
3. Paste this policy (replace bucket name):

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::dhanush-portfolio-2024/*"
        }
    ]
}
```

4. Click **Save** ✅

---

## **Step 5: Test Your Website**

Your website is now live! 🎉

- **Direct URL:** `http://dhanush-portfolio-2024.s3-website-ap-south-1.amazonaws.com`
- Click around, test the Home/Projects navigation
- Verify all links work

---

## **Step 6: (Optional) Use a Custom Domain**

If you have your own domain (e.g., `dhanush.dev`):

### **Using Route 53 (AWS)**

1. Go to **Route 53 Console**
2. Create hosted zone for your domain
3. Create **A record** pointing to your S3 bucket
4. Update nameservers at your domain registrar

### **Using Third-Party Domain Registrar**

1. Create **CNAME record** pointing to:
   - `dhanush-portfolio-2024.s3-website-ap-south-1.amazonaws.com`
2. Update at your registrar (GoDaddy, Namecheap, etc.)

---

## **Step 7: (Optional) Add HTTPS with CloudFront**

For better security and performance:

1. Go to **CloudFront Console**
2. Create distribution pointing to your S3 bucket
3. Request free SSL certificate via ACM
4. CloudFront provides HTTPS URL

---

## **Updating Your Portfolio**

When you make changes:

### **Via Console:**
1. Upload updated files to S3 bucket (overwrite existing)
2. Changes live in ~5 minutes

### **Via CLI:**
```bash
aws s3 cp index.html s3://dhanush-portfolio-2024/
aws s3 cp projects.html s3://dhanush-portfolio-2024/
```

---

## **Troubleshooting**

| Issue | Solution |
|-------|----------|
| 404 when accessing bucket | Check bucket policy allows public read access |
| Files not updating | S3 takes time to propagate, try incognito window |
| Can't find Static Website Hosting option | It's under **Properties** tab, scroll to bottom |
| "Access Denied" errors | Make sure bucket policy is configured |

---

## **Estimated Costs**

- **S3 Storage:** ~$0.01/month for your portfolio
- **Data Transfer:** Free tier covers most traffic
- **CloudFront (optional):** ~$0.085 per GB transferred

**Total: Essentially FREE for most use cases** ✅

---

## **What's Included in Your Portfolio**

✅ **Home Page (index.html)**
- Professional intro with contact links
- 4+ years experience summary
- Work experience at Infosys (2 roles)
- Education section
- Comprehensive skills with 8 categories
- Beautiful animations and responsive design

✅ **Projects Page (projects.html)**
- AWS Multi-VPC Architecture project with full technical details
- Current role details (Service Desk Operations)
- Previous role (Data Operations)
- Learning roadmap section
- Technical highlights and achievements

✅ **Navigation**
- Fixed header with Home/Projects links
- Active page indicator
- Responsive mobile design
- Smooth scrolling

✅ **Design**
- Modern dark theme with blue accents
- Fully responsive (desktop, tablet, mobile)
- Smooth animations and hover effects
- Professional typography
- No external dependencies (pure HTML/CSS/JS)

---

## **Next Steps**

1. Deploy to S3 using steps above
2. Test the live URL thoroughly
3. Share URL on LinkedIn, GitHub profile
4. Consider adding a blog section later
5. Keep your portfolio updated as you learn Docker, Kubernetes, Terraform

---

## **Quick Reference**

```bash
# Create bucket
aws s3 mb s3://dhanush-portfolio-2024 --region ap-south-1

# Upload files
aws s3 sync . s3://dhanush-portfolio-2024 --exclude "*" --include "*.html"

# List bucket contents
aws s3 ls s3://dhanush-portfolio-2024/

# Remove bucket (if needed)
aws s3 rm s3://dhanush-portfolio-2024/ --recursive
aws s3 rb s3://dhanush-portfolio-2024/
```

---

## **Support & Resources**

- AWS S3 Docs: https://docs.aws.amazon.com/s3/
- Static Website Hosting: https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html
- Bucket Policies: https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucket-policies.html

---

**Your portfolio is production-ready. Let's get it live! 🚀**

For questions or updates, you have everything you need right here in the HTML files.

---

*Built with care • Ready for the cloud*
