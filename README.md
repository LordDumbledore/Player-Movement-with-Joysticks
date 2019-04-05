# Player-Movement-with-Joysticks
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerMovment : MonoBehaviour
{
	public Joystick MovementJoystick;
	public Joystick cameraJoystick;
	public Rigidbody player;
	public CharacterController playerC;

	protected Vector3 moveDirection;
	public float Speed = 10f;
	protected float gravityScale;
	protected float vertSpeed;
	protected float horiSpeed;
	protected Vector3 playerPosition;
  
	private void Update()
	{
		moveDirection = ((transform.forward * MovementJoystick.Vertical) * Speed) + ((transform.right * MovementJoystick.Horizontal) * Speed);
		moveDirection.y = moveDirection.y + (Physics.gravity.y * gravityScale * Time.deltaTime);
		playerC.Move(moveDirection * Time.deltaTime);

		playerPosition = player.transform.position;
		playerPosition.y = 0;
		player.transform.position = playerPosition;



		vertSpeed -= cameraJoystick.Vertical * 2;
		horiSpeed += cameraJoystick.Horizontal * 4;

		player.transform.eulerAngles = new Vector3(vertSpeed, horiSpeed, 0.0f);
	}
}
