# triangle-blaster
Python Processing sketch involving triangles

To view this sketch you will need to download Processing from https://processing.org/download
Follow the steps on this page to install Python Mode for processing: https://www.geeksforgeeks.org/how-to-set-up-python-mode-for-processing/
Then copy and paste the following code into the editor and run:


def setup():
    
    fullScreen()
    frameRate(30)
    background(255)
    rectMode(CENTER)
    
def draw():
    
    halfwidth = width/2
    halfheight = height/2
    
    # The ultimate range of the triangles (expressed as distance from center)
    j = width/2 
    
    time_rate = 0.2 
    t = millis() * time_rate
    
    # Math stuff to get a triangle wave which will control
    # the growing and shrinking of triangles
    triangle_wave = j - abs( (t%(2*j))-j ) 
    
    # The triangle vertices are stored as values chosen at random 
    # from a range between the output of the triangle_wave function
    # and the negative of the output
    # (Both x and y values will be chosen from this list, so there are 6 items.)
    vertex_list = []
    for i in range(6):
        vertex_list.append(random(-triangle_wave, triangle_wave))
        
    #A simpler triangle wave to determine stroke weight.
    sw = abs(10-millis()%20)
    strokeWeight(sw)
    
    #Draw the **** triangle
    blendMode(DIFFERENCE)
    fill(random(255),random(255),random(255))
    stroke(255)
    triangle(halfwidth + vertex_list[0],
             halfheight + vertex_list[1],
             halfwidth + vertex_list[2],
             halfheight + vertex_list[3],
             halfwidth + vertex_list[4],
             halfheight + vertex_list[5])
    
    #A full-window rectangle used as mask to fade out drawn triangles.
    blendMode(ADD)
    noStroke()
    fill(255,7) #2nd number is alpha value
    rect(halfwidth, centerY, width+2, height+2)
