# Axeman
int axemanWidth, axemanHeight;
int axemanXpos, axemanYpos;
int axemanXvel, axemanYvel;
int logWidth, logHeight;
int logXpos, logYpos;
int logXvel, logYvel;
int fall = -100;
int random = (int)random(450);
int score;

float colliderXpos, colliderYpos;
float colliderRadius;
float colliderXpos2, colliderYpos2;
float colliderRadius2;

//(a class i cant figure out) logX;
PImage axeman;
PImage log;
PImage grass;
PImage sky;
PImage GameOver;

void setup() {
  size(500,500);
  //axeman stuff
  axemanWidth = width/3;
  axemanHeight = height/3;
  axemanXpos = width/3;
  axemanYpos = 325;
  axemanXvel = 5;
  axemanYvel = 0;
  colliderRadius = axemanWidth / 4.0;
  //log stuff
  logWidth = width;
  logHeight = height;
  logXpos = random;
  logYpos = fall;
  logXvel = 5;
  logYvel = 0;
  colliderRadius2 = logWidth / 4.0;
  axeman = loadImage("axey.gif");
  grass = loadImage("grass.gif");
  log = loadImage("LOg.gif");
  sky = loadImage("sky.gif");
  GameOver =loadImage("Game over screen 2.gif");
}


void draw() {
  background(0,0,0);
  fill(255,255,0);
  image(sky, 0, 0, 500, 500);
  colliderXpos= axemanXpos + axemanWidth/2 - 10;
  colliderYpos= axemanYpos + axemanHeight/2;
  //axeman circle
  ellipse(colliderXpos, colliderYpos, axemanWidth/2, axemanHeight/2);
  image(axeman, axemanXpos, axemanYpos, axemanWidth, axemanHeight);
  //log circle
  ellipse(random+ 75 , fall + 100 , 75, 75 );
  image(log, random , fall, 200, 200 );
  image(grass, 0, 400, 500, axemanHeight);
  fall = fall + 10;
  if (keyPressed){
    if (keyCode == RIGHT) {
      axemanXpos = axemanXpos + axemanXvel;
    }
    if (keyCode == LEFT) {
      axemanXpos = axemanXpos - axemanXvel;
    }
  }
  
  //log reset
  if ( fall > 400 ){
    fall= 0;
    random = (int)random(450);
    score= score +1;
   }
  if (axemanXpos >= width){
    axemanXpos = width-1;
  }
  if (axemanXpos <= 0){
    axemanXpos = 1;
  }
  if (axemanYpos <= 0 || axemanYpos >= height){
    axemanYvel = -axemanYvel;
  }
  
  if(dist(colliderXpos, colliderYpos, random, fall) < colliderRadius) {
    print("Collided"); 
    image(GameOver, 0, 0, 500, 500);
    noLoop();
  }
}
