# Hover Recruitment Code Challenge

Thank you for taking the time to complete this challenge. 

## Task requirements

- Feel free to spend as much time on this as you like, the time you spend working on it and how it long it takes you to submit are NOT considered in the review. It is meant to take 4-8 hours to complete and we recommend not taking more than a week to submit it. You may use any internet sources.
- Complete the user stories below
- You may use any dependencies you like
- When finished, ZIP the code and share it with us. It does not need to contain a built APK, but we must be able to build the APK from source using gradle without any errors. Please do not share publicly on Github.
- The Hover team is standing by to provide technical support if neccessary

## Problem statement

Hover's technology requires identifying SIM cards so that the correct USSD and SIM Toolkit services are run on the right networks. There is no official and always up-to-date record of networks in every country, so it would be helpful to compare what a user's SIM card is reporting vs what information Hover has listed.

The Hover Android SDK has a dual-SIM library built into it (we are in the process of [separating and open-sourcing it](https://github.com/UseHover/MultiSim)). It simplifies getting SIM info across different devices and Android versions, especially on dual SIM devices. For this exercise assume that the information it gives is accurate: you do NOT need to test yourself on a dual SIM device.

For now it is easiest to use through the Hover SDK. You don't need a Hover account, just include the following in your app:

1. Add the Hover repo to your root build.gradle repositories:
<figure><pre><code>
allprojects { 
	repositories {
		...
		mavenCentral()
		maven { url "http://maven.usehover.com/releases" }
	}
}
</code></pre></figure>

2. Add the Hover SDK to your app-level build.gradle dependencies:

<figure><pre><code>
dependencies {
	...
	implementation 'com.hover:android-sdk:1.4.1'
}
</code></pre></figure>

Get the READ_PHONE_STATE permission from the user, then call `Hover.updateSimInfo(context)` which will populate the library's SIM database. Then you can use the static methods on the SimInfo object to load them from the database. Documentation can be found in the [javadoc](http://maven.usehover.com/releases/com/hover/android-sdk/1.4.1/android-sdk-1.4.1-javadoc.jar).

Hover provides its list of network operators via a public HTTP API: https://www.usehover.com/api/world_operators. This endpoint provides the name, country alpha2, mobile country code (MCC) and mobile network codes (MNCs) of each network. The MCC + MNC together are called the Home Network Identifier (HNI) and are also the first 5-6 digits of the IMSI. [Wikipedia]{https://en.wikipedia.org/wiki/Mobile_country_code) has a useful summary and list. Hover also provides a list of countries for completeness: https://www.usehover.com/api/countries.

## User stories

- As a user I want to see in my app which SIM card(s) are present in my device.
- As a user I want to compare what the MultiSim library is reporting to what Hover's network list reports as the name and country of my SIM card.
- As a user I want to submit a request to update the information for my SIM card. 
  - There is no real url for this, but just assume you are delivering some JSON to an endpoint. The JSON schema should make sense and provide the neccessary info to understand what the user thinks the network should be as well as what the phone is reporting.

## Acceptance criteria

- Does your solution fully meet the user requirements and are any edge cases or errors handled.
- Does your code show mastery of basic object oriented design and clean code principles.
- Test coverage
- Documentation
- You will not be graded on UI/UX (That is what designers are for!) but basic readability of the interface is still important.
