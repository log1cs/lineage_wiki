## Basic requirements

1. Read through the instructions at least once before actually following them, so as to avoid any problems due to any missed steps!
2. You actually want to upgrade your device to the newest version - if you wish to downgrade to an earlier version of LineageOS, follow your [device's]({{ device | device_link: "/install" | relative_url }}) instructions for installing LineageOS the first time.

{%- if device.before_install.instructions == "needs_specific_android_fw" %}
{% unless device.before_install.ships_fw %}
{% capture path %}templates/device_specific/before_install_{{ device.before_install.instructions }}.md{% endcapture %}
{% include {{ path }} %}
{% endunless %}
{%- endif %}

## Manually upgrading LineageOS

The updater app does not support upgrades from one version of LineageOS to another, and will block installation to any update for a different version. Upgrading manually requires similar steps to installing LineageOS for the first time.

1. Verify your device is using the latest [Lineage Recovery](https://download.lineageos.org/devices/{{ device.codename }}). Simply download the latest recovery file, named `boot.img`.
Follow your [device's installation guide]({{ device | device_link: "/install" | relative_url }}) to see how you can update your recovery image.
    {% include alerts/important.html content="These instructions may not work if you choose to use a different recovery!" %}
2. Download super_empty.img image [here](https://download.lineageos.org/devices/NB1/builds).
3. In recovery mode, select `Advanced` and then select `Enter fastboot`.
4. Run `fastboot wipe-super --slot=all /path/to/super_empty.img` to flash `super_empty` image.
    {% include alerts/note.html content="You only need to do this once when upgrading from LineageOS 21 to LineageOS 22.1." %}
    {% capture content -%}
    If you get the following error: `fastboot: usage: unknown command wipe-super`, make sure [ADB and fastboot are updated to the latest version]({{ "adb_fastboot_guide.html" | relative_url }}). You need fastboot version 28.0.2 or greater.
    {%- endcapture %}
    {%- include alerts/note.html content=content %}
5. Back to the phone, select `Enter recovery`.
6. Download the [LineageOS install package](https://download.lineageos.org/devices/NB1) that you'd like to install or [build]({{ device | device_link: "/build" | relative_url }}) the package yourself.
7. If you are currently using (or now want to use) an application package add-on such as [Google Apps]({{ "gapps" | relative_url }}), you have the following options:
    - keep using them: Download the appropriate version [now]({{ "gapps" | relative_url }}) (use the `arm64` architecture)
    - remove them: You can only do so by performing a [factory reset]({{ "glossary/#factory-reset" | absolute_url }}){: .glossary}, which will also remove all your data.
    - start using them: You can only do so by performing a factory reset, which will also remove all your data. Download the appropriate version [now]({{ "gapps" | relative_url }}) (use the `arm64` architecture)
8. Make sure your computer has working `adb`. Setup instructions can be found [here]({{ "adb_fastboot_guide.html" | relative_url }}).
9. Click `Advanced`, then `Enable ADB`.
10. Run `adb -d reboot sideload`.
    {% include alerts/important.html content="The device may reboot to a blank black screen, fear not, this is a known bug on some recoveries, proceed with the instructions." %}
11. Run `adb -d sideload /path/to/zip` (inserting the path to your LineageOS package).
    {% include alerts/specific/tip_adb_flash_success.html %}
12. _(Optionally)_: If you want to install any add-ons, click `Advanced`, then `Reboot to Recovery`, then when your device reboots, click `Apply Update`, then `Apply from ADB`, then `adb -d sideload /path/to/zip` those packages in sequence.
    {% include alerts/note.html content="If you previously had any Google Apps add-on package installed on your device, you must install an updated package **before** the first boot of Android! If you did not have Google Apps installed, you must wipe the **Data** partition (or perform a factory reset) to install them." %}
    {% include alerts/specific/note_signature_check.html %}
13. Once you have installed everything successfully, click the back arrow in the top left of the screen, then "Reboot system now".

## Get assistance
After you've double checked that you followed the steps precisely, didn't skip any and still have questions or got stuck, feel free to ask on [our subreddit](https://reddit.com/r/LineageOS) or in
[#LineageOS on Libera.Chat](https://web.libera.chat/gamja/?channel=#lineageos).