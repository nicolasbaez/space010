## : : s p a c e 0 1 0

![space](https://github.com/nicolasbaez/space010/blob/master/space010.gif)

```processing
int vert[]=new int[360];
int vx[]={3, 4, 5, 6, 8, 9, 10, 12, 15, 18, 20, 24, 30, 36, 40, 45, 60, 72, 90};
int rr[]=new int[360];
int gg[]=new int[360];
int bb[]=new int[360];
int st[]=new int[360];
float rot[]=new float[360];
float rotStart[]=new float[360];
int frame=0;
void setup() {
  size(512, 256, P3D);
  for (int i=0; i<360; i++) {
    vert[i]=vx[int(random(vx.length))];
    rr[i]=int(random(255));
    gg[i]=int(random(255));
    bb[i]=int(random(255));
    st[i]=int(random(128, 255));
    rot[i]=random(1);
    rotStart[i]=0;
  }
}
float dRot=0;
void draw() {
  float radio=height*0.125;
  background(0);
  for (int i=0; i<360; i+=5) {
    fill(rr[i], gg[i], bb[i], 64);
    stroke(st[i]);
    pushMatrix();
    rotateX(radians(i+dRot));
    translate(width*0.5, height*0.75);
    beginShape();
    for (float j=rotStart[i]; j<=360+rotStart[i]; j+=int(360/vert[i])) {
      float xx=radio*cos(radians(j));
      float yy=radio*sin(radians(j));
      vertex(xx, yy);
    }
    endShape();
    popMatrix();
    rotStart[i]+=rot[i];
  }
  dRot+=0.18;
  if (dRot<360) {
    saveFrame("gif/space010-######.png");
  }
}
```
