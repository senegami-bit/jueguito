# 🟦 Game Title: Spike Sprint

# 👥 Team: George Mena, Uriel Aguilar

# 🎮 Game Description:
Spike Sprint is a fast-paced obstacle game inspired by Geometry Dash and The Impossible Game. 
The player controls the cube to jump over obstucles and dangerous spikes. 
The goal is to try to complete the levels without dying and collecting 3 coins on levels.

# Mechanics used:
Automatic foward movement
Up-Arrow, Space Bar or Mouse click
Collision detection on obstucles
Restarting on player's death
Level Progression
Coin collecting

# 📦 Resources Used (ASSETS and Sprites)

 # Images
![image of the player icon](https://i.pinimg.com/474x/dd/b4/b2/ddb4b288d3eb1b7b669e77e3d21f9566.jpg)

![image of the platform or block](https://static.wikia.nocookie.net/geometry-dash/images/0/01/RegularBlock01.png/revision/latest?cb=20160604070948)

![image of the spike](https://tiermaker.com/images/media/template_images/2024/16361404/gd-spike-tier-list-16361404/screenshot20231120-203009-997.png)

![image of the coin](https://image.pngaaa.com/688/3664688-middle.png)
 


# 🗺️ Scene Descriptions
Tutorial/Level 1:
![Screenshot 2025-07-06 192724](https://github.com/user-attachments/assets/965011c2-30ca-4f23-b697-0b2e5156d486)

Basic Movement and jumping over blocks, introducing the game mechanic for jumping.


# Level 2:
![Screenshot 2025-07-05 123928](https://github.com/user-attachments/assets/8dac073a-7f4b-462b-a07f-ff7eb011a764)

Spikes are introduced and makes the level harder to pass, jumping over obstucles and collecting 3 coins on hard areas.
Death: Player dies, shows the area where they died and restarts the level to the beginning.
Player: Icon rotates on jumping or falling

# Player/Character

![Screenshot 2025-07-06 193225](https://github.com/user-attachments/assets/6327272a-ed35-479a-92fd-4703ebe86850)

# Spike/Enemy

![Screenshot 2025-07-06 193255](https://github.com/user-attachments/assets/c3fe70bd-96a4-4269-8793-53d2a7297cab)

# Platform/Block

![Screenshot 2025-07-06 193237](https://github.com/user-attachments/assets/c5f2d3e4-7e04-4b44-8230-6c5642f06cf1)

# Coin

![Screenshot 2025-07-06 193304](https://github.com/user-attachments/assets/5226dbcc-d903-499c-9e73-00424de33a8e)


# 🧑‍💻 Code Descriptions

- Character/Player code


      extends CharacterBody2D


      const SPEED = 35500
      const JUMP_VELOCITY = -1000

      var gravedad = 4100

      func _physics_process(delta: float) -> void:
	  #gravedad
	  if not is_on_floor():
		velocity += get_gravity() * delta

	  #salto
	  if Input.is_action_pressed("salto") and is_on_floor():
		velocity.y = JUMP_VELOCITY

	  velocity.x = SPEED * delta

	  move_and_slide()

      $Sprite2D.rotation_degrees += 380 * delta
	  else :
		var modulo = int($Sprite2D.rotation_degrees) % 90;
	
		if modulo > 45 :
			$Sprite2D.rotation_degrees += (90 - modulo)
		else :
			$Sprite2D.rotation_degrees -= modulo

  
  - Spike code
   
        extends Area2D

        func _on_body_entered(body):
	    if body.is_in_group("kill") :
		$"..".death()
		self.queue_free()
  
y para externo muerte:

    extends Area2D

    func _on_area_entered(area: Area2D) -> void:
	if area.is_in_group("kill") :
		$"..".death()
		self.queue_free()
  
(tambien hizo un cambio del jugador para un nuevo hitbox de muerte para los pinchas (spikes):)

    func death():
	SPEED = 0
	$Sprite2D.visible = false
	$Timer.start()
 
- Transitions

      func _on_timer_timeout() -> void:
	  get_tree().reload_current_scene()

      func _on_puerta_body_entered(body: Node2D) -> void:
	  get_tree().change_scene_to_file("res://escenario/NIVEL2.tscn")
	  pass # Replace with function body. 

# 🛠️ Difficulties Encountered Using Collaborative Tools

 George: I had difficulty running the game and had issues with assets not working. It took me 30 mins to figure out how to collect coins and make the player speed
 and gravity to be perfect. For the coin, I couldn't figure how to collect coin to be labeled on the top left.


 Uriel:
I had problems on the animations for a transition, at first, I did the coding for the transition and it worked, however, it was glitching on Level 2
Then, I figured out that the Collsion Size for the transition needs to be on top of the level.


# Conclusion

It was a very long process trying to make the game to function. Git showed us coding and transfer codes to others easily without losing progress.
Also, it took days to find the perfect code to make it function well and without any errors. Next time, we will use other ways to send files easily without losing progrss.
