# FinalExamProject
class Star{
  float x;
  float y;
  float z;
  
  float pz;
  
  Star(){
    x = random(-width, width);
    y = random(-height, height);
    z = random(width);
    pz = z;
  }
  
  void update(){
    z = z - speed;
    if (z <1){
    z = width;
    x = random(-width, width);
    y = random(-height, height);
    pz = z;
    //^decides the location of the stars starting point
  }
 }
  void show(){
    fill(255);
    noStroke();
    //^makes the stars white

    float sx = map(x / z, 0, 1, 0, width);
    float sy = map(y / z, 0, 1, 0, height);

    float r = map(z, 0, width, 16, 0);
    //ellipse(sx, sy, r, r);
    
    float px = map(x / pz, 0, 1, 0, width);
    float py = map(y / pz, 0, 1, 0, height);
    
    pz = z;
    stroke(255);
    line(px, py, sx, sy);
    //^moves the stars faster as the get closer to the edge
    
  
  }
}

Star[] stars = new Star[8000];
float speed;
//^starts the 'speed' varible
void setup(){
  size(800,800);
  //^decides the size of the stars visiblilty
  for (int i = 0; i < stars.length; i++){
    stars[i] = new Star();
  }
}
//draws the dots
void draw(){
  speed = map(mouseX, 0, width, 0, 15);
  //^speeds up the stars as you move your mouse to the right
  background(0);
  //^sets backround to black
  translate(width/2, height/2); 
  //^brings the stars moving around the center not the top corner
  for (int i = 0; i < stars.length; i++){
    stars[i].update();
    stars[i].show();
    //^updates star location, and tells when to show them
  }
}
