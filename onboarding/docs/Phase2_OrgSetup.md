Company Info

Purpose: Sets org-wide locale, time zone, and currency so dates, times, and amounts render consistently for HR processes and reports.

Screenshot: Company Information page.

Metadata: Organization settings aren’t retrieved as a single file; they’re captured implicitly by org configuration and referenced in release notes. Note the chosen Locale, Time Zone, and Currency in the doc for auditability.
![alt text](image.png)
Business Hours and Holidays

Purpose: Defines HR’s working window for approvals, due times, and future SLA calculations; holidays ensure non‑working days are respected.

Screenshot: “HR Business Hours” detail and Holidays list.

![alt text](image-1.png)

Metadata: 
<?xml version="1.0" encoding="UTF-8"?>
<BusinessHoursSettings xmlns="http://soap.sforce.com/2006/04/metadata">
    <businessHours>
        <active>true</active>
        <default>true</default>
        <fridayEndTime>00:00:00.000Z</fridayEndTime>
        <fridayStartTime>00:00:00.000Z</fridayStartTime>
        <mondayEndTime>00:00:00.000Z</mondayEndTime>
        <mondayStartTime>00:00:00.000Z</mondayStartTime>
        <name>Default</name>
        <saturdayEndTime>00:00:00.000Z</saturdayEndTime>
        <saturdayStartTime>00:00:00.000Z</saturdayStartTime>
        <sundayEndTime>00:00:00.000Z</sundayEndTime>
        <sundayStartTime>00:00:00.000Z</sundayStartTime>
        <thursdayEndTime>00:00:00.000Z</thursdayEndTime>
        <thursdayStartTime>00:00:00.000Z</thursdayStartTime>
        <timeZoneId>America/Los_Angeles</timeZoneId>
        <tuesdayEndTime>00:00:00.000Z</tuesdayEndTime>
        <tuesdayStartTime>00:00:00.000Z</tuesdayStartTime>
        <wednesdayEndTime>00:00:00.000Z</wednesdayEndTime>
        <wednesdayStartTime>00:00:00.000Z</wednesdayStartTime>
    </businessHours>
    <businessHours>
        <active>true</active>
        <default>false</default>
        <fridayEndTime>18:00:00.000Z</fridayEndTime>
        <fridayStartTime>09:00:00.000Z</fridayStartTime>
        <mondayEndTime>18:00:00.000Z</mondayEndTime>
        <mondayStartTime>09:00:00.000Z</mondayStartTime>
        <name>HR Business Hours</name>
        <thursdayEndTime>18:00:00.000Z</thursdayEndTime>
        <thursdayStartTime>09:00:00.000Z</thursdayStartTime>
        <timeZoneId>America/Los_Angeles</timeZoneId>
        <tuesdayEndTime>18:00:00.000Z</tuesdayEndTime>
        <tuesdayStartTime>09:00:00.000Z</tuesdayStartTime>
        <wednesdayEndTime>18:00:00.000Z</wednesdayEndTime>
        <wednesdayStartTime>09:00:00.000Z</wednesdayStartTime>
    </businessHours>
</BusinessHoursSettings>


Fiscal Year

Confirmed Standard Fiscal Year with Start Month January and “Based on ending month” to keep analytics and dashboards in sync with HR’s calendar-year planning without enabling custom fiscal years.
![alt text](image-2.png)
Users

Ensured at least one HR test user for assignment of roles and permission sets during build and UAT; this enables realistic security testing early.
![alt text](image-3.png)

Profiles and Roles

Kept a standard profile for HR and established a minimal role hierarchy “CEO > HR Manager” to support top‑down visibility and approval routing while keeping administration simple.

Permission Set

Created “HR Onboarding Access” (empty baseline) to centralize future object/field/tab permissions without relying on profile proliferation; this follows permission‑set‑led security best practices.
![alt text](image-4.png)
App Manager

Created the “HR Onboarding” Lightning app with a clear brand color and starter navigation (Home, Accounts, Reports, Dashboards) so HR has a dedicated workspace; versioned as CustomApplication metadata for CI/CD.
![alt text](image-5.png)
Metadata:
<?xml version="1.0" encoding="UTF-8"?>
<CustomApplication xmlns="http://soap.sforce.com/2006/04/metadata">
    <brand>
        <headerColor>#1F7A8C</headerColor>
        <shouldOverrideOrgTheme>false</shouldOverrideOrgTheme>
    </brand>
    <description>Streamlines new-hire onboarding with standardized HR hours, approvals, and access setup across roles and permissions.</description>
    <formFactors>Small</formFactors>
    <formFactors>Large</formFactors>
    <isNavAutoTempTabsDisabled>false</isNavAutoTempTabsDisabled>
    <isNavPersonalizationDisabled>false</isNavPersonalizationDisabled>
    <isNavTabPersistenceDisabled>false</isNavTabPersistenceDisabled>
    <isOmniPinnedViewEnabled>false</isOmniPinnedViewEnabled>
    <label>HR Onboarding</label>
    <navType>Standard</navType>
    <tabs>standard-ApprovalsHome</tabs>
    <tabs>standard-Account</tabs>
    <tabs>standard-report</tabs>
    <tabs>standard-Dashboard</tabs>
    <uiType>Lightning</uiType>
    <utilityBar>HR_Onboarding_UtilityBar</utilityBar>
</CustomApplication>

Navigation Items
![alt text](image-6.png)

Manifest entries used for retrieval

Rationale: Ensures consistent retrieval of all Phase 2 components.
<Package xmlns="http://soap.sforce.com/2006/04/metadata">
  <types>
    <members>*</members>
    <name>Role</name>
  </types>
  <types>
    <members>BusinessHours</members>
    <name>Settings</name>
  </types>
  <types>
    <members>*</members>
    <name>CustomApplication</name>
  </types>
  <types>
    <members>*</members>
    <name>CustomTab</name>
  </types>
  <version>64.0</version>
</Package>


OWD: keep defaults; no Sharing Rules yet.

Login Access Policies: leave default