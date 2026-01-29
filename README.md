# Azure Lab: Conditional Access & Geographic Security Perimeters

## 📌 Project Overview
As I pivot from on-prem home labs (IPFire/Wazuh) into Cloud Security, this lab focuses on **Identity as the New Perimeter**. I implemented a Conditional Access (CA) policy in Azure Entra ID admin console to enforce geographic restrictions, ensuring that administrative access is only possible from approved "Named Locations."

##  Technical Stack
* **Cloud Provider:** Microsoft Azure
* **Identity Service:** Microsoft Entra ID (Azure AD)
* **Security Tool:** Conditional Access Policies
* **Focus:** Geo-blocking & Zero Trust Identity

## 🚀 The Build Process

### 1. Defining the Perimeter
I created a **Named Location** within Microsoft Entra ID. This allows the tenant to recognize specific IP ranges or countries as "Trusted" or "Targeted."
> ![Defining Geographic Network Perimeters](images/image1.png)

### 2. Policy Configuration
The policy logic was set to:
* **Who:** All users.
* **What:** All Cloud Apps.
* **Where:** Any location *except* my designated safe countries.
* **Result:** Block Access.
> *![Policy Configuration](images/image2.png)*

---

## ⚠️ Lessons Learned & Troubleshooting

### Disabling Security Defaults
One major hurdle I encountered: **You cannot use Conditional Access while "Security Defaults" are enabled.** * Security Defaults provide a basic level of protection but are an "all-or-nothing" setting. To use granular CA policies, these must be turned off.
* **Location:** `Overview` > `Properties` > `Manage Security Defaults` (at the bottom of the page).

### The Cache/Propagation Trap
**Critical Tip:** After disabling Security Defaults, Azure may still throw an error when you try to save your new CA policy. 
* **The Fix:** Don't panic and keep clicking save, you need to **log out, clear your browser cache, and log back in**. This forces the portal to recognize the updated tenant state and allows the policy to be created successfully.

---------------------------------------------------------------------

## 📈 Future Improvements
* Implement "What If" tool testing to simulate logins from blocked regions.
* Integrate Azure Monitor to visualize blocked sign-in attempts on a map.
* Layer MFA requirements on top of the Geo-block for "Trusted" locations.

**Author:** Benjamin Soko
