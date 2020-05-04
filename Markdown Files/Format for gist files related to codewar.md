[<p align="left"><img width="267" height="150" src="https://img.youtube.com/vi/r7yOMz8HrHk/maxresdefault.jpg"></p>](https://youtu.be/r7yOMz8HrHk)
## Straight Line Examples using C/C++ graphics.h
<h4>Example 1</h4>
<p align="center">
    <img width="443" height="350" src="https://raw.githubusercontent.com/rp181135198/My-Gist-Files-Data/master/Image%20Data/Straight%20Line%20Examples%20in%20C%2B%2B%20graphics.h/Example%20of%20lineto%20and%20moveto.PNG"><br>
    <b>Using lineto and moveto functions</b><br>
</p>

```
#include<graphics.h>
#include<math.h>
#define MAXPTS	15

struct PTS {
  int x, y;
};	/* Structure to hold vertex points	*/
double AspectRatio;		/* Aspect ratio of a pixel on the screen*/

void LineToDemo(void)
{
    struct PTS points[MAXPTS];
    int i, j, h, w, xcenter, ycenter;
    int radius, angle, step;
    double  rads;

    h = getmaxy();
    w = getmaxx();

    xcenter = w/2;			/* Determine the center of circle */
    ycenter = h/2;
    radius  = (h-30)/(AspectRatio*2);
    step	= 360/MAXPTS;		/* Determine # of increments	*/

    angle = 0;				/* Begin at zero degrees	*/
    for( i=0 ; i<MAXPTS ; ++i ){		/* Determine circle intercepts	*/
        rads = (double)angle * M_PI / 180.0;	/* Convert angle to radians	*/
        points[i].x = xcenter + (int)( cos(rads) * radius );
        points[i].y = ycenter - (int)( sin(rads) * radius * AspectRatio );
        angle += step;			/* Move to next increment	*/
    }

    circle( xcenter, ycenter, radius );	/* Draw bounding circle 	*/

    for( i=0 ; i<MAXPTS ; ++i ){		/* Draw the cords to the circle */
        for( j=i ; j<MAXPTS ; ++j ){	/* For each remaining intersect */
        moveto(points[i].x, points[i].y); /* Move to beginning of cord	*/
        lineto(points[j].x, points[j].y); /* Draw the cord		*/
        }
    }

// Main function
int main()
{
    int gd=DETECT,gm;
    initgraph(&gd,&gm,(char*)"");

    int xasp,yasp;
    getaspectratio( &xasp, &yasp );	// read the hardware aspect
    AspectRatio = (double)xasp / (double)yasp; // Get correction factor
    
    LineToDemo();
    
    getch();
    closegraph();
    return 0;
}
```

<h4>Example 2</h4>
<p align="center">
    <img width="443" height="350" src="https://raw.githubusercontent.com/rp181135198/My-Gist-Files-Data/master/Image%20Data/Straight%20Line%20Examples%20in%20C%2B%2B%20graphics.h/Example%20of%20linerel%20and%20moverel.PNG"><br>
    <b>Using linerel and moverel functions</b><br>
</p>
