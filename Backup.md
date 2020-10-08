//Create variables here
var dog, happyDog;
var dogImage;
var database;
var foodS, foodStock;

function preload()
{
  dogImage = loadImage("images/dogImg.png");
  happyDog = loadImage("images/dogImg1.png");
}

function setup() {
  createCanvas(500, 500);
  dog = createSprite(250, 250, 40, 40);
  dog.addImage("normalDog", dogImage);
  dog.scale = 0.4; 
  foodStock = database.ref('Food');
  foodStock.on("value", readStock);
}


function draw() {  
  background(46, 139, 87);
  if(keyWentDown(UP_ARROW)){
    writeStock(foodS-=1);
    dog.addImage(happyDog)
  }
  drawSprites();
  //add styles here
  textSize(20);
  fill(255);
  stroke(10);
  text(foodStock, 20, 20);
  text("Press The UP Arrow Key To Feed The Dog Milk!", 250, 10);


}
function readStock(data){
  foodS = data.val();
}
 function writeStock(x){
   database.ref('/').update({
     Food:x
   })
 }