---
title: "Rename your custom Management Packs"
date: "2013-02-04"
excerpt_separator: "<!--More-->"
categories: 
  - "operations-manager"
tags: 
  - "microsoft"
  - "operations-manager"
  - "system-center"
---

When importing a new Management Pack, a custom Management pack should always be created for containing overrides for det imported Management Pack. This is not just a good idea, it´s also Microsoft best practice. The reason why we do this is to separate all of the overrides for our imported Management Packs. Instead of having to clean up our Default Management Pack after deleting a MP, e.g. Exchange Server 2007 is thrown out to be replaced by Exchange Server 2010, just delete the Exchange Server 2007 Overrides MP. Sometimes when implementing SCOM, a naming standard is not in place for the Management Packs and the Override MP´s are just randomly named. Below is how to change the display name and actual name of the MP. This method requires that the Override MP is exported and then deleted from the SCOM console, edited using Notepad and then again imported via the SCOM console.
<!--More-->
### Editing the Management Pack

For this post I have just used notepad for editing the MP.

The key items to change are <Name> ,  <ID> & <LanguagePack Details ElementID= and <Name>

The Original Override MP Element ID name was: **Override.Group.Policy.xml**

And the old display name was: **Override Group Policy**

The New Element ID name will be: **Orneling.Group.Policy.Overrides**

and the New Display name will be: **Orneling - Group Policy – Overrides**

I have highlighted the changes made in the XML of the Group Policy Override Management Pack as an example.

**Note:** Also note that once you have made and saved the changes you must make sure the MP filename is the same as the **Element ID** name so the filename for this pack will be **Orneling.Group.Policy.Overrides.xml**

```

<?xml version=”1.0″ encoding=”utf-8″?>
<ManagementPack ContentReadable=”true” xmlns:xsd=”http://www.w3.org/2001/XMLSchema&#8221; xmlns:xsl=”http://www.w3.org/1999/XSL/Transform”&gt;
<Manifest>
<Identity>
<ID>Orneling.Group.Policy.Overrides</ID>
<Version>2.0.0.0</Version>
</Identity>
<Name>Orneling – Group Policy – Overrides</Name>
<References>
<Reference Alias=”SystemCenter”>
<ID>Microsoft.SystemCenter.Library</ID>
<Version>6.0.6278.0</Version>
<PublicKeyToken>31bf3856ad364e35</PublicKeyToken>
</Reference>
<Reference Alias=”Windows”>
<ID>Microsoft.Windows.Library</ID>
<Version>6.0.6278.0</Version>
<PublicKeyToken>31bf3856ad364e35</PublicKeyToken>
</Reference>
<Reference Alias=”Windows1″>
<ID>Microsoft.Windows.Server.GroupPolicy.2003</ID>
<Version>6.0.6278.22</Version>
<PublicKeyToken>31bf3856ad364e35</PublicKeyToken>
</Reference>
</References>
</Manifest>
<Monitoring>
</Monitoring>
<LanguagePacks>
<LanguagePack ID=”ENG” IsDefault=”false”>
<DisplayStrings>
<DisplayString ElementID=”Orneling.Group.Policy.Overrides“>
<Name>Orneling – Group Policy – Overrides</Name>
<!–DisplayString>
</DisplayStrings>
<!–LanguagePack>
<LanguagePack ID=”ENU” IsDefault=”false”>
<DisplayStrings>
ElementID=”Orneling.Group.Policy.Overrides“>
<Name>Orneling – Group Policy – Overrides</Name>
</DisplayString>
</DisplayStrings>
</LanguagePack>
</LanguagePacks>
</ManagementPack>
```

### Exporting your custom made Management Packs

To export your unsealed Managegement Packs and also for backing them up on a daily basis, refer to my post here.