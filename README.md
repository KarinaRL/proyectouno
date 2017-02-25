# proyectouno
 import ddf.minim.*;
Minim soundengine;
AudioSample sonido1;
ArrayList<PVector> points = new ArrayList<PVector>();
  Flock flock;
 Eye e1,e2, e3,e4,e5,e6;

 int g=0;
 int x=100;
 int x1=700;
 boolean presionandogato = false; 
boolean presionandoperro = false;

int estado=0;


void setup(){
  size(800,600,P3D);
     soundengine = new Minim(this);
  sonido1 = soundengine.loadSample("we.mp3", 1024);
   sonido1.trigger();
   noFill();
fondo();
//MOVIMIENTO DE OJOS
 e1 = new Eye( 96,  234, 25);
 e2 = new Eye( 145, 234, 25);  
 e3 = new Eye( 96,  234, 25);
 e4 = new Eye( 145, 234, 25);
e5 = new Eye( 120, 240, 25);
     e6 = new Eye( 650, 240, 25); //
}

void draw(){
  background(0);
if(estado==0){
  voton();
fecha();
letrero();
  flock.run();
}
  if(estado==1){
  gato();
  letrero2();
  letrero3();
  perro();  
}
if (estado==2){
   
   verificarBotones();
   gato_perfil();
    perro_perfil();
}

}

void letrero(){

String [] titulo = {"CAT","VS","DOG"};
  PFont e= createFont("Goudy Stout",30);
colorMode(HSB);
textSize(10);
textFont (e);
text(titulo[0],200,200); 
text(titulo[1],400,300); 
text(titulo[2],500,400); 
}
void letrero2(){
String [] titulo = {"Elige","una","Mascota"};
  PFont e= createFont("Goudy Stout",15);
colorMode(HSB);
textSize(10);
textFont (e);
fill(#EDA50A);
text(titulo[0],250,200); 
text(titulo[1],350,300);
text(titulo[2],400,400); 
}
void letrero3(){
String [] titulo = {"Gato","Perro"};
  PFont e= createFont("Goudy Stout",20);
colorMode(HSB);
textSize(10);
textFont (e);
fill(255);
text(titulo[0],87,560); 
text(titulo[1],630,560);
}


void fondo(){
    flock = new Flock();
  for (int i = 0; i < 150; i++) {
    flock.addBoid(new Boid(width/2,height/2));

}
}

void fecha(){
  
  int dia= day();
int mes= month();
int ao= year();
int posicionyreloj=40;
textSize(20);
String s=String. valueOf(dia);
text(s,10,posicionyreloj);

s=String.valueOf(mes);
text ('/'+ s,40,posicionyreloj);

s=String.valueOf(ao);
text ('/'+s,70,posicionyreloj);

}

void voton(){
  fill(255);
  int cx=300;
  int cy=500;
  int dcx=100;
  int dcy=65;
  if (mousePressed){
    if((mouseX>=dcx|| mouseY>dcx) && (mouseX>dcy|| mouseY>dcy)){
              print("a");
          estado=1;
    }
  }
 }
 void voton2(){
   int a=20;
   int c=130;
   int td=210;
   int te=390;
   fill(#1BF5EF);
  stroke(255);
  strokeWeight(10);
  rect(a,c,td,te,70,70,50,50);
  if (mousePressed){
 if ((mouseX<td||mouseY<td)&&(mouseX<te||mouseY<te))       
      estado=2;
  }
    if (mousePressed){      
     
  }
 }
//ELEGIR PERSONAJES

void gato(){
 voton2();
  //orejas
  stroke(#232727);
    fill(0);
  arc(100,200,100,100,HALF_PI+QUARTER_PI,PI+QUARTER_PI);
    arc(140,200,100,100,PI+HALF_PI+QUARTER_PI,TWO_PI+QUARTER_PI);
    //caveza
     fill(0);
    ellipse(120,250,115,102);
    noStroke();
     //nariz
    fill(#FC9CE1);
    arc(120,265,40,40,PI+QUARTER_PI,PI+HALF_PI+QUARTER_PI);
     //patitas traseras 
    fill(#1F1818);
     rect(60,350,50,90,70,70,50,50);
     rect(140,350,50,90,70,70,50,50);
     fill(#484444);
     rect(60,430,40,18,70,70,50,50);
     rect(150,430,40,18,70,70,50,50);
     //cuerpo
     fill(0);
     rect(85,300,80,150,70,70,50,50);
    //patitas delanteras
    fill(#343131);
    ellipse(110,450,35,20);
    ellipse(150,450,35,20);
      e1.update(mouseX, mouseY);
   e2.update(mouseX, mouseY);

  e1.display();
  e2.display();
 
}

void perro(){
   translate(550,8);
  fill(#9EBC19);
  stroke(255);
  strokeWeight(10);
  rect(20,130,210,390,70,70,50,50);
  //orejas
    fill(0);
    noStroke(); 
    rotar();
    rotate(radians(-10));
    //caveza
     fill(0);
    ellipse(120,250,115,102);
    noStroke();
     //nariz
    fill(#FC9CE1);
    arc(120,265,40,40,PI+QUARTER_PI,PI+HALF_PI+QUARTER_PI);
     //patitas traseras 
    fill(#1F1818);
     rect(60,350,50,90,70,70,50,50);
     rect(140,350,50,90,70,70,50,50);
     fill(#484444);
     rect(60,430,40,18,70,70,50,50);
     rect(150,430,40,18,70,70,50,50);
     //cuerpo
     fill(0);
     rect(85,300,80,150,70,70,50,50);
    //patitas delanteras
    fill(#343131);
    ellipse(110,450,35,20);
    ellipse(150,450,35,20);
      e3.update(mouseX, mouseY);
   e4.update(mouseX, mouseY);
   
  e3.display();
  e4.display();
  
    
}
void rotar(){

rotate(radians(10));
ellipse(100,240,20,100);
ellipse(220,240,20,100);
}

class Eye {
  
  int x, y;
  int size;
  float angle = 0.0;
  
  Eye(int tx, int ty, int ts) {
    x = tx;
    y = ty;
    size = ts;
 }

  void update(int mx, int my) {
    angle = atan2(my-y, mx-x);
  }
  
  void display() {
    pushMatrix();
    translate(x, y);
    fill(255);
    ellipse(0, 0, size, size);
    rotate(angle);
    fill(#1BF5EF);
    ellipse(size/4, 0, size/2, size/2);
    popMatrix();
  }
}
//
 
 
 

 
 //fondo
 
 class Flock {
  ArrayList<Boid> boids;

  Flock() {
    boids = new ArrayList<Boid>(); 
  }

  void run() {
    for (Boid b : boids) {
      b.run(boids); 
    }
  }

  void addBoid(Boid b) {
    boids.add(b);
  }

}


class Boid {

  PVector position;
  PVector velocity;
  PVector acceleration;
  float r;
  float maxforce;   
  float maxspeed;    

    Boid(float x, float y) {
    acceleration = new PVector(0, 0);

    float angle = random(TWO_PI);
    velocity = new PVector(cos(angle), sin(angle));

    position = new PVector(x, y);
    r = 4.0;
    maxspeed = 4;
    maxforce = 0.01;
  }

  void run(ArrayList<Boid> boids) {
    flock(boids);
    update();
    borders();
    render();
  }

  void applyForce(PVector force) {
  
    acceleration.add(force);
  }

  
  void flock(ArrayList<Boid> boids) {
    PVector sep = separate(boids);  
    PVector ali = align(boids);      
    PVector coh = cohesion(boids);   

    sep.mult(1.5);
    ali.mult(1.0);
    coh.mult(1.0);
   
    applyForce(sep);
    applyForce(ali);
    applyForce(coh);
  }
  void update() {
   
    velocity.add(acceleration);
    velocity.limit(maxspeed);
    position.add(velocity);
    acceleration.mult(0);
  }

// Un método que calcula y aplica una fuerza de dirección hacia un objetivo
  // STEER = MENOR VELOCIDAD DESEADA
  PVector seek(PVector target) {
    PVector desired = PVector.sub(target, position);  
    desired.normalize();
    desired.mult(maxspeed);

    PVector steer = PVector.sub(desired, velocity);
    steer.limit(maxforce);  // Limit to maximum steering force
    return steer;
  }

  void render() {
    float theta = velocity.heading2D() + radians(90);
    
    fill(random(255), random(255),random(255));
    stroke(0,0,random(255));

    pushMatrix();
    translate(position.x, position.y);
    rotate(theta);
    beginShape(TRIANGLES);
    vertex(0, -r*2);
    vertex(-r, r*2);
    vertex(r, r*2);
    endShape();
    popMatrix();
  }

  // Wraparound
  void borders() {
    if (position.x < -r) position.x = width+r;
    if (position.y < -r) position.y = height+r;
    if (position.x > width+r) position.x = -r;
    if (position.y > height+r) position.y = -r;
  }

  PVector separate (ArrayList<Boid> boids) {
    float desiredseparation = 25.0f;
    PVector steer = new PVector(0, 0, 0);
    int count = 0;
 
    for (Boid other : boids) {
      float d = PVector.dist(position, other.position);
      
      if ((d > 0) && (d < desiredseparation)) {
        PVector diff = PVector.sub(position, other.position);
        diff.normalize();
        diff.div(d);        
        steer.add(diff);
        count++;        
      }
    }
    if (count > 0) {
      steer.div((float)count);
    }

// Siempre que el vector sea mayor que 0
    if (steer.mag() > 0) {
      steer.normalize();
      steer.mult(maxspeed);
      steer.sub(velocity);
      steer.limit(maxforce);
    }
    return steer;
  }

  PVector align (ArrayList<Boid> boids) {
    float neighbordist = 50;
    PVector sum = new PVector(0, 0);
    int count = 0;
    for (Boid other : boids) {
      float d = PVector.dist(position, other.position);
      if ((d > 0) && (d < neighbordist)) {
        sum.add(other.velocity);
        count++;
      }
    }
    if (count > 0) {
      sum.div((float)count);
      sum.normalize();
      sum.mult(maxspeed);
      PVector steer = PVector.sub(sum, velocity);
      steer.limit(maxforce);
      return steer;
    } 
    else {
      return new PVector(0, 0);
    }
  }
 
  PVector cohesion (ArrayList<Boid> boids) {
    float neighbordist = 50;
    PVector sum = new PVector(0, 0);   
    int count = 0;
    for (Boid other : boids) {
      float d = PVector.dist(position, other.position);
      if ((d > 0) && (d < neighbordist)) {
        sum.add(other.position); 
        count++;
      }
    }
    if (count > 0) {
      sum.div(count);
      return seek(sum);  
    } 
    else {
      return new PVector(0, 0);
    }
  }
}
void gato_perfil(){
  noStroke();
    fill(0);
  arc(110,200,100,100,HALF_PI+QUARTER_PI,PI+QUARTER_PI);
    arc(120,200,100,100,HALF_PI+QUARTER_PI,PI+QUARTER_PI);
    //caveza
     fill(0);
    ellipse(120,250,100,102);
    noStroke();
     //nariz
    fill(#FC9CE1);
    arc(160,265,40,40,PI+QUARTER_PI,PI+HALF_PI+QUARTER_PI);
     //patitas traseras 
    e5.update(mouseX, mouseY);
  e5.display();
}
void perro_perfil(){
  noStroke();
    fill(0);
    arc(120,200,100,100,HALF_PI+QUARTER_PI,PI+QUARTER_PI);
    //caveza
     fill(0);
    ellipse(650,250,100,102);
    ellipse(600,250,50,60);
       fill(#33383B);
    ellipse(690,250,50,80);
    noStroke();
     //nariz
    fill(#FC9CE1);
    arc(590,240,40,40,PI,PI+HALF_PI);
     //patitas traseras 
    e6.update(mouseX, mouseY);
  e6.display();
}

void keyPressed(){
   if(key == 'z' || key == 'Z' ){
    presionandogato = true;
  }
  if(key == 'm' || key == 'M' ){
    presionandoperro = true;
  }  
}
void keyReleased (){
   if(key == 'z' || key == 'Z' ){
    presionandogato = false;
    x=100;
  }
  if(key == 'm' || key == 'M' ){
    presionandoperro = false;
    x1=700;
  }
}

void verificarBotones(){
  //vida de gato
  int tam1=10;
int tam2=100;
for(int x1=0; x1<300; x1+=tam1){ 
 rect(x1,500,tam1,tam2);
 if(x<300){
   x1=x1-tam1;
  }
}
 
  //vida de perro
 int tam3=10;
int tam4=100;
for(int i=500; i<800; i+=tam3){ 
  fill(#184B71);
 rect(i,500,tam3,tam4);
 if(x<300){
   x=x-tam3;
  }
 
}
  
  if (presionandogato == true){
    fill(#19E7F7);
    ellipse(x,400,100,100);
    x=x+5;

  }  
  if (presionandoperro == true){
    fill(#184B71);
    ellipse(x1,400,100,100);
    x1=x1-5;
  }
}
