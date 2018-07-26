# Font Awesome Custom

## How to add new icon
1. Go to [icomoon.io](https://icomoon.io/app/#/projects)
2. Click on **Import Project** and import the latest [Smartkarma - Font Awesome.json](https://drive.google.com/open?id=1l5vpNyoekHp1cugKiCu91b0-rdcNEOQm)
3. Click **Load** to open the project in IcoMoon
4. Select icons that you want to export
5. If you want to import your custom SVG icon, click **Import Icons** and select the icon when it's imported to the project
6. After you have selected all the icons that you want, click **Generate Font**
7. Click **Download** to download the `.zip` file
8. Paste `style.css` and `fonts` folder into `sk-common/vendors/font-awesome-custom/` folder
9. `.woff2` file isn't generated, so you need to use a converter tool like [Font Converter](https://www.font-converter.net/en) to convert `.ttf` to `.woff2`

## Tips

1. **Ligatures** -
An icon can be represented as a word called ligatures. Currently, only smartkarma logo is set to have a ligature: `smartkarma`

2. **Preferences** -
You can change the `.zip` file settings by clicking the *gear* icon next to the **Download** button.
There you can change the CSS class for icons, font names and it's also possible to generate `.scss` instead of `.css` file

3. **Adding new custom font** -
Add new icons to `Smartkarma - custom` collection and not into `Font Awesome` collection for easier future upgrades
