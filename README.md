# Website Setup Instructions

These instructions will guide you through how to set up a new website on your local machine using LocalWP while utilising Composer to manage plugins. This solution came about because managing plugins via git is a nightmare. WordPress doesn't have to be a massive pain, and while the setup process in these instructions is longer than just the default method, you'll thank yourself in the long run.

## Requirements 

- [Local WP](https://localwp.com/) -- Local WordPress development made simple.
- [SpinupWP Composer Site](https://github.com/spinupwp/spinupwp-composer-site) -- WordPress site setup using Composer that is primed and ready to be hosted using SpinupWP.
- [SpinupWP](https://spinupwp.app/) -- Modern Cloud-Based Server Control Panel.
- A theme of some sort. I recommend [Sage 10](https://docs.roots.io/sage/10.x/installation/#installing-sage-with-composer) or [Understrap](https://github.com/understrap/understrap) if you're not ready to dive into Sage 10. [Underscores](https://github.com/Automattic/_s) is another good option if you don't want Bootstrap or Tailwind.
-[This .gitignore file](https://gist.github.com/mattneal-stafflink/9e0ad8d4b4ad18b4cf82503d93c6255f) or your own version.

## Getting Started 

1. Create a new site in LocalWP. I recommend Nginx, PHP 8.0+, and MySQL 8.0.16. SpinupWP has deprecated its support for MariaDB.
2. Rename the `public` directory that was created by LocalWP. You can delete it but don't lose the wp-config! Rename it to `public_backup` or similar.
3. From the `app` folder, run `composer create-project spinupwp/spinupwp-composer-site public`. This will download and set up WordPress in a more suitable structure for Composer.
4. Update the `.gitignore` file with the one mentioned above in the requirements.
5. Edit the `.env` file in the new `public` directory and update the database settings with the wp-config.php from the `public_backup` folder (the original directory that LocalWP created).
6. Update `WP_HOME` to be that of the local url you created. (Eg http://spinuptest.local )
7. Open the `site.conf.hbs` file in the `nginx` folder which is adjacent to the `app` folder that LocalWP created (NOT the app folder that composer create-project created).
8. Change the Line `root   "{{root}}”;` to be `root   "{{root}}/public";`. This tells LocalWP where the root DIR for the website is, since we've changed the structure by using the Spinup Composer Site repo.
9. Enable SSL for this site through LocalWP, then trust the new SSL in your keychain on Mac.
10. Open the site shell, navigate to the public directory, and activate your theme. `wp theme activate theme-name` e.g. `wp activate twentytwentyone`.

## Development

You can now do what you gotta do to make a sweet lookin' website!

When you are ready to go live, you can either use a plugin, or manually updload it to SpinupWP first. Once you've got the site up, don't forget to hook up your new git repo to your SpinupWP site.
