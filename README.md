# Codeigniter-Config-Writer
Permanently update config values using [this library here](https://github.com/hollax/ArrayConfigWriter)

watch video here [here](https://www.youtube.com/watch?v=5pEjs3cyDec&feature=youtu.be)
## STEPS
   1 Download the library https://github.com/hollax/ArrayConfigWriter and extract it under libraries folder of your codeigniter project
   
   2 Create a new class under your libraries folder, name it as prefered, e.g Config_Writer
   
   3 Inside the the class you created, include the library class
   
   require_once APPPATH . 'libraries/array_config_writer/class-array-config-writer.php';

    /**
     * Get instance of the config writer
     * 
     * @param string $file Absolute path to config file , default to the main config file
     * @param string $variable_name The name of varible(array) that holds items 
     * @return \Array_Config_Writer
     */
    public function get_instance( $file = null , $variable_name = 'config' )
    {
        if(!$file)
        {
            $file = APPPATH.'config/config.php';
            
        }
        return new Array_Config_Writer( $file , $variable_name );
    }
    
You can start usinng the library to update the config items 

## USAGE

     $this->load->library('config_writer');
     //to write the main config file, omit the argument
     $writer = $this->config_writer->get_instance();
     $writer->write('compress_output' , true );
     
If you check the compression config option, it should now be set to true


      /*
      |--------------------------------------------------------------------------
      | Output Compression
      |--------------------------------------------------------------------------
      |
      | Enables Gzip output compression for faster page loads.  When enabled,
      | the output class will test whether your server supports Gzip.
      | Even if it does, however, not all browsers support compression
      | so enable only if you are reasonably sure your visitors can handle it.
      |
      | VERY IMPORTANT:  If you are getting a blank page when compression is enabled it
      | means you are prematurely outputting something to your browser. It could
      | even be a line of whitespace at the end of one of your scripts.  For
      | compression to work, nothing can be sent before the output buffer is called
      | by the output class.  Do not 'echo' any values with compression enabled.
      |
      */
      $config['compress_output'] = true;
        
##To update the db configuration  

       $this->load->library('config_writer');
       //to write the main config file, omit the argument
       // notice that the first argument points to the database config file and 
       //the second argument is the $db config variable name in the file
       $writer = $this->config_writer->get_instance( APPPATH.'config/database.php', 'db');
       // to update the host name
       $writer->write( array('default' , 'hostname' ) , 'thehostname' );
  Check the database.php config file, you should see
  
        $db['default']['hostname'] = 'thehostname';
        
Another use case is , updating language file.

I use this library to manage my codeigniter project languages.
