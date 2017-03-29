unit fighter;

{$mode objfpc}{$H+}

interface

uses
  Classes, SysUtils, FileUtil, Forms, Controls, Graphics,
  Buttons, ExtCtrls, FPImage, intfGraphics, LCLType, LResources;

type

  { TForm1 }

  TForm1 = class(TForm)
    bmFighter: TBitmap;
    bmBackground: TBitmap;
    bmBlack: TBitmap;
    bmMeteor: TBitmap;
    bmBlackMeteor: TBitmap;
    bmOver: TBitmap;
    bmBanner: TBitmap;
    bmBoom: TBitmap;
    bmHighScore: TBitmap;

    digit:TBitmap;


    Timer1: TTimer;
    Timer2: TTimer;

    procedure FormCreate(Sender: TObject);
    procedure FormMouseDown(Sender: TObject);
    procedure FormMouseUp(Sender: TObject);
    procedure FormPaint(Sender: TObject);
    procedure Timer1Timer(Sender: TObject);
    procedure Timer2Timer(Sender: TObject);

  private
    { private declarations }
  public
    { public declarations }
  end;

var
  Form1: TForm1;
  fighterposx, fighterposy, speed, speedm, accelerator, meteorx, meteory, flag, i,k: integer;
  score:longint;
  gameover: boolean;
  s:string;

implementation

procedure TForm1.FormCreate(Sender: TObject);
begin
  gameover := False;
  randomize;

  speed := 0;
  speedm:= 0;
  score := 0;
  flag:= 0;

  bmFighter := TBitmap.Create;
  bmFighter.LoadFromFile('sprites\fighter.bmp');
  bmBackground := TBitmap.Create;
  bmBackground.LoadFromFile('sprites\sky.bmp');
  bmBlack := TBitmap.Create;
  bmBlack.LoadFromFile('sprites\black.bmp');
  bmMeteor := TBitmap.Create;
  bmMeteor.LoadFromFile('sprites\meteor.bmp');
  bmBlackMeteor := TBitmap.Create;
  bmBlackMeteor.LoadFromFile('sprites\blackmeteor.bmp');
  bmOver := TBitmap.Create;
  bmOver.LoadFromFile('sprites\banner.bmp');
  bmBanner := TBitmap.Create;
  bmBanner.LoadFromFile('sprites\banner.bmp');
  bmBoom := TBitmap.Create;
  bmBoom.LoadFromFile('sprites\boom.bmp');
  bmHighScore := TBitmap.Create;
  bmHighScore.LoadFromFile('sprites\HighScore.bmp');

  fighterposx := 50;
  fighterposy := 240;
  meteorx := 640;
  meteory := random(410);

end;


procedure TForm1.FormMouseDown(Sender: TObject);
begin
  speedm:=10;
  if fighterposy > 0 then
    speed := 1
  else
    speed := 0;
end;


procedure TForm1.FormMouseUp(Sender: TObject);
begin
  accelerator := 0;
  if fighterposy < 480 then
    speed := -2
  else
    speed := 0;
end;

procedure TForm1.FormPaint(Sender: TObject);
begin
  canvas.Draw(0, 0, bmBackground);
  canvas.Draw(fighterposx, fighterposy, bmFighter);
  canvas.Draw(meteorx, meteory, bmMeteor);
  canvas.Draw(120,100, bmBanner);
end;


procedure TForm1.Timer1Timer(Sender: TObject);
begin
  if (speed > 0) and (accelerator < 3) then
    accelerator := accelerator + 1;

  if (gameover = False) and (speed<>0) then
  begin
    canvas.Draw(fighterposx, fighterposy, bmBlack);
    fighterposy := fighterposy - (speed + accelerator);
    canvas.Draw(fighterposx, fighterposy, bmFighter);
  end;

  if (speed<>0) and (score=0) and (flag=0) then
      begin
          canvas.Draw(0, 0, bmBackground);
          canvas.Draw(fighterposx, fighterposy, bmFighter);
          canvas.Draw(meteorx, meteory, bmMeteor);
      end;
  if (score<999999) and (speed>0) then score:=score+1;
end;


procedure TForm1.Timer2Timer(Sender: TObject);
begin
  if ((meteorx <= 20) and (fighterposy < meteory + 150) and (fighterposy > meteory - 27)) or
    (fighterposy < 0) or (fighterposy > 480) then
    gameover := True;
  if (meteorx < 0) and (gameover = False) and (speedm <>0) then
  begin
    canvas.Draw(meteorx, meteory, bmBlackMeteor);
    meteorx := 640;
    meteory := random(410);
  end;
  if gameover = False then
  begin
    canvas.Draw(meteorx, meteory, bmBlackMeteor);
    meteorx := meteorx - speedm;
    canvas.Draw(meteorx, meteory, bmMeteor);
  end
  else
       if Flag =0 then
           begin
             canvas.Draw(fighterposx, fighterposy, bmBoom);
             canvas.Draw(200, 200, bmHighScore);
             for i:=1 to 6 do
                begin
                  s:='sprites\';
                  digit:= TBitmap.Create;
                  k:=score mod 10;
                  case k of
                  1:s:=s+'1.bmp';
                  2:s:=s+'2.bmp';
                  3:s:=s+'3.bmp';
                  4:s:=s+'4.bmp';
                  5:s:=s+'5.bmp';
                  6:s:=s+'6.bmp';
                  7:s:=s+'7.bmp';
                  8:s:=s+'8.bmp';
                  9:s:=s+'9.bmp';
                  else s:=s+'0.bmp'
                  end ;
                  digit.LoadFromFile(s);
                  canvas.Draw(450-i*30,250,digit);
                  digit.free;
                  score:=score div 10;
                end;
             Flag:=1;
           end;
end;


initialization
   {$I fighter.lrs}

end.

