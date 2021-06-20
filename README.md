
# Description

Installation of GTK+3.0 on Red Hat Enterprise Linux 8.4

# Installation

```$ sudo yum groupinstall "Development Tools" ```

``` $ sudo yum install gtk3-devel ```

In order to show if gtk is correctly installed show pkg-config list result :
 
``` $ pkg-config --list-all | grep gtk ```
 
You must obtain a result like this :

```
gtk+-3.0                       GTK+ - GTK+ Graphical UI Library

gtk+-broadway-3.0              GTK+ - GTK+ Graphical UI Library

gtk+-unix-print-3.0            GTK+ - GTK+ Unix print support

gtk+-wayland-3.0               GTK+ - GTK+ Graphical UI Library

gtk+-x11-3.0                   GTK+ - GTK+ Graphical UI Library
```

# Testing

Create a main.c file with the code below :
 ``` c {
#include <gtk/gtk.h>
 
static void
activate (GtkApplication* app,
           gpointer        user_data)

   GtkWidget *window;
 
   window = gtk_application_window_new (app);
   gtk_window_set_title (GTK_WINDOW (window), "Window");
   gtk_window_set_default_size (GTK_WINDOW (window), 200, 200);
   gtk_widget_show_all (window);
  }
  
 int
 main (int    argc,
       char **argv)
 {
   GtkApplication *app;
   int status;
 
   app = gtk_application_new ("org.gtk.example", G_APPLICATION_FLAGS_NONE);
   g_signal_connect (app, "activate", G_CALLBACK (activate), NULL);
   status = g_application_run (G_APPLICATION (app), argc, argv);
   g_object_unref (app);
 
   return status;
 }
 ```

 ## Compilation

 Compile the code with gcc 
 
 ```
 $ gcc main.c -o main -Wall `pkg-config --cflags gtk+-3.0` `pkg-config --libs gtk+-3.0`
 ```
