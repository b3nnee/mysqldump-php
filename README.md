# MySQLDump - PHP

This replicates mysqldump in terminal "$ mysqldump -u username -p..."

## Installation

Install mysqldump using artisan:

    php artisan bundle:install mysqldump

Then in your *application/bundles.php* file, add the following line to load Resizer automatically:

    return array(
        'mysqldump' => array( 'auto' => true )
    );

Or without the `'auto' => true` to load it on demand:

    return array(
        'mysqldump'
    );

## Usage

<?php

class Cron_Controller extends Base_Controller
{
    public function get_backup()
    {
        Bundle::start('mysqldump');
        $conn = Config::get('database.connections.mysql');

        $filename = time() . ".sql";
        $filepath = "storage/work/";

        $dump = new MySQLDump();
        $dump->host     = $conn['host'];
        $dump->user     = $conn['username'];
        $dump->pass     = $conn['password'];
        $dump->db       = $conn['database'];
        $dump->filename = $filepath . $filename;
        $dump->start();

        return "Backup complete.";
    }
}

## Credits

This was originally written by someone in 2009, I just OOP'd it out a lot more and simplify it.

Enjoy.
