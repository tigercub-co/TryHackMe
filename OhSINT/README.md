# OhSINT

## Initial Image
In This box we start by downloading an image off the Try Hack Me Site when the image is downloaded you can open the image and it looks like just the default Windows XP Background

![XP Background](https://github.com/tigercub-co/TryHackMe/blob/master/OhSINT/images/WindowsXP.jpg)

As when the image was opened there is no extra information to be viewed so we will exiftool the file to see if that results in any extra information which can be seen below.

![exif information](https://github.com/tigercub-co/TryHackMe/blob/master/OhSINT/images/exif.JPG)

From that it shows that there is Copyright information OWoodflint. So using that information we will google that name to see if any extra information is found. When doing a google search it comes back with three main results a [twitter page,](https://twitter.com/owoodflint?lang=en) a [blog page](https://oliverwoodflint.wordpress.com/author/owoodflint/) and a [github page](https://github.com/OWoodfl1nt)

## Twitter page

The first page we will look at is OWoodflint's twitter page which has only two posts but includes an avatr of a cat.

![Twitter Page](https://github.com/tigercub-co/TryHackMe/blob/master/OhSINT/images/twitter.JPG)

*Answer A Cat Avatar*

One of those posts gives important information of a BSSID of B4:5D:50:AA:86:41 so we can use that information to find an exact location of his home.
With that information we can search for the BSSID on [wigle](https://wigle.net/) once on that page we can search for that BSSID.

![Location of BSSID](https://github.com/tigercub-co/TryHackMe/blob/master/OhSINT/images/BSSID.JPG)

*Answer London is the home location of OwoodFlint*
We can then zoom in on that BSID to find out the SSID of that BSSID.

![SSID MAp Image](https://github.com/tigercub-co/TryHackMe/blob/master/OhSINT/images/SSID.JPG)

*Answer UnileverWiFi is the SSID of BSSID*

## Github page
We can now look at the github page of OwoodFlint as we have gathered all the infomration needed from his twitter page. Using the github page it shows that he has one project within called people finder

![Github Page](https://github.com/tigercub-co/TryHackMe/blob/master/OhSINT/images/GithubPage.JPG)

We can then look at this project and within it shows OwoodFlints email

![people finder page](https://github.com/tigercub-co/TryHackMe/blob/master/OhSINT/images/Github.JPG)

*Answer OwoodFlints email is OWoodflint@gmail.com*
*Answer Location where we found the email is github*

## Blog Page
As all that was on the github page has been found after research we can move to look at OwoodFlints Blog Page

![OwoodFlints web page](https://github.com/tigercub-co/TryHackMe/blob/master/OhSINT/images/Blog.JPG) 

*Answer OwoodFlints Holiday was to New York*
But looking at the questions we know that we still have to find OwoodFlints password so one of the ways we could do this is to look at the source code of the page

![OwoodFlints web page Source Code](https://github.com/tigercub-co/TryHackMe/blob/master/OhSINT/images/password.JPG)

We can see that there was text which was trying to be hidden which was the same colour as the background.
*Answer OwoodFlints password is pennYDr0pper.!*
