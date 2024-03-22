# (community) Framework Grub Theme
GRUB2 bootloader theme for the Framework laptop

![](https://upload.wikimedia.org/wikipedia/commons/7/7b/Framework_Computer_logo.svg)

## Installing
Move the content of this repo into a folder called framework in your grub theme folder. Typically this is /boot/grub/themes/framework.

## Configuring
Be sure to enable the theme, and set the correct screen size in the grub default config file. Typically this is found at /etc/default/grub.

``` /etc/default/grub
GRUB_GFXMODE=2560x1600x32
GRUB_THEME="/boot/grub/themes/framework/theme.txt"
```

## Features
Countdown timer is shown on space key and by removing segments of the Framework logo. Space bar on background image is also a countdown progress bar.

Icons are included for popular linux distributions as well as generic grub icons. Found near [vinceliuice](https://github.com/vinceliuice/grub2-themes)

Boot menu scroll bar is the framework gear, themed with colors from background image.

Background image originally created by [StephenMauriceGraham](https://twitter.com/400facts/status/1647910740416667650)
![](https://pbs.twimg.com/media/Ft6M7rdXoAI39DZ?format=jpg&name=large)

## Help requests
 - Polish on graphics
   - transparencies and detail work
   - A re-drawn original 2560x1600 background image
     - Make laptop screen in background fit grub's minimum console dimensions
   - Other official 2560x1600 background image

## Notes
If you want all the boot select icons to appear, you will need to modify your grub config to support the `--class` menu flag.

```
diff --git a/10_linux b/home/techtruth/10_linux
index 70d69fc..2f60aa0 100755
--- a/10_linux
+++ b/home/techtruth/10_linux
@@ -95,11 +95,9 @@ linux_entry ()
       case $type in
          recovery)
              title="$(gettext_printf "%s, with Linux %s (recovery mode)" "${os}" "${version}")"
-             recovery_tag="--class recovery"
            ;;
          *)
              title="$(gettext_printf "%s, with Linux %s" "${os}" "${version}")"
-             recovery_tag=""
            ;;
       esac
       if [ x"$title" = x"$GRUB_ACTUAL_DEFAULT" ] || [ x"Previous Linux versions>$title" = x"$GRUB_ACTUAL_DEFAULT" ]; then
@@ -108,7 +106,7 @@ linux_entry ()
          title_correction_code="${title_correction_code}if [ \"x\$default\" = '$quoted' ]; then default='$(echo "$replacement_title" | grub_quote)'; fi;"
          grub_warn "$(gettext_printf "Please don't use old title \`%s' for GRUB_DEFAULT, use \`%s' (for versions before 2.00) or \`%s' (for 2.00 or later)" "$GRUB_ACTUAL_DEFAULT" "$replacement_title" "gnulinux-advanced-$boot_device_id>gnulinux-$version-$type-$boot_device_id")"
       fi
-      echo "menuentry '$(echo "$title" | grub_quote)' ${recovery_tag} ${CLASS} \$menuentry_id_option 'gnulinux-$version-$type-$boot_device_id' {" | sed "s/^/$submenu_indentation/"
+      echo "menuentry '$(echo "$title" | grub_quote)' ${CLASS} \$menuentry_id_option 'gnulinux-$version-$type-$boot_device_id' {" | sed "s/^/$submenu_indentation/"
   else
       echo "menuentry '$(echo "$os" | grub_quote)' ${CLASS} \$menuentry_id_option 'gnulinux-simple-$boot_device_id' {" | sed "s/^/$submenu_indentation/"
   fi
@@ -300,7 +298,7 @@ for linux in ${reverse_sorted_list}; do
        boot_device_id="$(grub_get_device_id "${GRUB_DEVICE}")"
     fi
     # TRANSLATORS: %s is replaced with an OS name
-    echo "submenu '$(gettext_printf "Advanced options for %s" "${OS}" | grub_quote)' --class submenu \$menuentry_id_option 'gnulinux-advanced-$boot_device_id' {"
+    echo "submenu '$(gettext_printf "Advanced options for %s" "${OS}" | grub_quote)' \$menuentry_id_option 'gnulinux-advanced-$boot_device_id' {"
     is_top_level=false
   fi
   ```


I've also put my email in some of the image comments. :^)
