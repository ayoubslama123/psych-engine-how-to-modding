Start By search This In PlayState.hx : public var cameraSpeed:Float = 1; 
And type after this code that :
  var ableToDodge:Bool = false;
	var dodging:Bool = false;
	var dodgeTimer:Float = 0.22625;
	var dodgeCooldown:Float = 0.1135;
	var alert:FlxSprite;
  after that search This : super.create();
  
  and type : 
  ableToDodge = true;
  
  after that search This : CustomFadeTransition.nextCamera = camOther;
  and type :
  function dodge(ableToDodge:Bool = false){
	if(curSong.toLowerCase() == 'your-song'){
		if(ableToDodge){
			FlxG.sound.play(Paths.sound('your-sound'));
			FlxG.cameras.flash(FlxColor.RED, 0.5);
			FlxG.cameras.shake(0.05, 0.5);
		new FlxTimer().start(0.09, function(tmr:FlxTimer){
			if (!dodging){
				FlxG.sound.play(Paths.sound('a-error-sound'));
				health -= 10069;
			}
		});
		}
		else{
			FlxG.sound.play(Paths.sound('the-kill-sound'));
		}
		}
}
function dodgeWarn(warnCanAppear:Bool = false){
	if(warnCanAppear){
		alert.animation.play('the-animation-name');
		FlxG.sound.play(Paths.sound('warn-sound'));
	}
}

search this : super.update(elapsed);
and type :
if (curSong.toLowerCase() == "your-song"){
			if(FlxG.keys.justPressed.SPACE && !dodging && ableToDodge){
				dodging = true;
				boyfriend.playAnim('dodge');
				boyfriend.debugMode = true;
				boyfriend.holdTimer = 0.7;
			new FlxTimer().start(dodgeTimer, function(tmr:FlxTimer)
                {
                dodging = false;
                boyfriend.dance();
				});
			new FlxTimer().start(0.7, function(tmr:FlxTimer)
				{
				boyfriend.debugMode = false;
				});
			new FlxTimer().start(dodgeCooldown, function(tmr:FlxTimer) 
				{
					ableToDodge = true;
				});
			}
		}
    
    search this code : callOnLuas('onStepHit', []);
    and type after this code that:
    if (curSong.toLowerCase() == "your-song"){
			switch (curStep){
				case 90:
					add(alert);
					dodgeWarn(true);
				case 95:
					dodgeWarn(true);
				case 100:
					dodge(true);
			}
	}
  
  now go to your song state and add this :
  alert = new FlxSprite().loadGraphic(Paths.image('your-image'));
				alert.cameras = [camHUD];
				alert.y = 205;
				alert.x = FlxG.width - 700;//your positions
				alert.antialiasing = ClientPrefs.globalAntialiasing;
				alert.setGraphicSize(Std.int(alert.width * 1.5));//if you want it to be bigger or more tiny use this
				alert.frames = Paths.getSparrowAtlas('your-image');//the png and xml you are going to use
				alert.animation.addByPrefix('the-animation-name', 'anim-in-xml', 24, false);//your anim name and xml
