# Sign In and Password Reset

**Sequence:** 21  
**Source:** MVP Requirements / Sign In and Password Reset #ClientUser  
**ClickUp Page ID:** 8cp80ab-4995  
**Last Updated:** 2025-12-15  
**Tags:** #ClientUser

---

### 1\. Sign In
1. WHAT:
    1. See [static designs](http://Get Started now Back  Next Sign in to your Account Get Started now Enter your email and password  Enter your Organisation name Enter your email and password to log in  Email Organization Name Email localloop@gmail.com localloop@gmail.com localloop@gmail.com Password Password ******* ******* Forgot Password ? Next By registering, you confirm that you are authorized to share business data on behalf of your organization. All data will be kept confidential, used only to provide feedback to you/your Organization or for anonymized aggregated analysis, and never shared without explicit consent. We comply fully with UK GDPR and store all data securely. Log In Description Or Or Continue with QuickBooks Read full Terms & Conditions Continue with QuickBooks Continue with Xero Back  Join  Continue with Xero Already have an account? Login Already have an account? Login Don’t have an account? Sign Up Forgot Password Reset Password Enter your Email Enter and confirm your new password Email New Password localloop@gmail.com ******* Confirm Password ******* Forgot Password  Reset Password  Already have an account? Login Already have an account? Login) for interface.
    2. Functional requirements:
        1. Sign in:
            1. As per v1.1/1.2.
            2. Sign-in should be logged and trigger any appropriate 'user session' actions
        2. Password reset
            1. As per v1.1/1.2.

### 9\. Additional testing notes
*   Tickets with relevant testing scripts:
    *   1315; 760; 894; 947

*       *   ![](https://t9015918923.p.clickup-attachments.com/t9015918923/eece2bdb-fe49-422d-8d21-f967aee7318f/Screenshot%202025-08-11%20at%2016.08.55.png)

**Board clean-up notes**
*   Tickets that can be closed because their testing scripts are relevant, but captured by #1315:
    *   1211
*   Tickets that can be closed as obsolete:
    *   664; 882; 896; 948; 1052; 704

### 10\. Post-MVP notes
1. Sign-in should trigger and update any 'novice user' actions.
2. 2FA?
3. Problems signing in?
    1. Link on Landing/Sign-in page: 'Problems signing in?' leads to sign-in problems page (or popover - design dependency), with:
        1. "Forgotten Password" link
            1. Password reset is secure, straightforward, logical and as simple as practical, implemented by typical sequence: ask for email, send transactional email with password reset button.
        2. "Other Problems" link
            1. Leads to 'Contact Us' page (design dependency)
###   

###

---

**Document Metadata:**
- **Created:** 2025-07-14
- **Sequence Number:** 21
- **Source System:** ClickUp
- **Workspace ID:** 9015918923
- **Doc ID:** 8cp80ab-3995
- **Page ID:** 8cp80ab-4995
