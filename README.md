# Intro To VR: Assignment 1

## Goals
- Get course development environement setup
- Build Familiarity with Unity Concepts
- Iron out the kinks of mobile deployment

## Setup
Download and install [Unity Hub](), this will let you install multiple Unity versions and manage your projects. You will have to make a free Unity account before you can start developing.

Once you have your basic environment setup, create a new project with Unity Hub. Hit the big blue **NEW** button in the upper right, make sure **3D** is selected on your left, then give your project an appropriate name and location on your computer.

## Creating a Simple Scene
Click on your project in Unity Hub to open it. If you have never used Unity before, take a moment to familiarize yourself with the editor once Unity boots up. Here are some resources that might help you get acquainted.
- [Basic Interface Overview](https://docs.unity3d.com/Manual/LearningtheInterface.html)
- [Interface Overview Video](https://www.youtube.com/watch?v=D7v2pjke5sc)
- [GameObjects and Components Video](https://www.youtube.com/watch?v=9Nf2_ds5y8c)
- [About an Hour of Interface Overviews](https://learn.unity.com/tutorial/using-the-unity-interface?courseId=5c8bcd60edbc2a0020e41e6d#)

[The Unity Manual](https://docs.unity3d.com/Manual/index.html) is also a pretty detailed resource.

### Let's Add Something to the Scene
Look at the sample scene in inspector
Game objects
Creating One
Adding a script to it

## Deploying
Now that you have an scene to deploy, let's get you set up to run it on your phone. First close Unity since we will be adding new libraries. Follow the setup guide for the type of phone you have. You can add moduals to your Unity installation by going to the **Installs** tab in Unity Hub, and clicking on the 3 dots on the version you are using, then selecting **Add Modules**.
- [Android](https://docs.unity3d.com/Manual/android-sdksetup.html)
- [IOS](https://learn.unity.com/tutorial/building-for-mobile#5c7f8528edbc2a002053b4a1)

## Let's Make it Interactive!
We are going to make it so that when you tap the screen, a ball shoots out from the center. First we will have to make a **Prefab** for the ball. Prefabs are templates for objects that we can create at runtime, they make it easy to create a lot of really similar objects. To turn the ball into a prefab, simply drag it into the project area at the bottom of the window next to the scenes folder.

Select the BallPrefab and you should see it show up on the right side of the inspector. From here we can edit our default values for all future instances of the prefab. For now, just add the **Rigidbody** component to give our ball physics.

Now let's create a new script and attach it to the main camera, name it *BallShooter*. In the BallShooter script let's add a public variable. Right above the `start` method add this line of code
```
public BallPrefab ball;
```
With public variables we can set values in a script from the editor to make them easy to change on the fly. Now let's add the code that makes our balls shoot. In the `update` method of *BallShooter* add the following:
```
if(Input.GetMouseButtonDown(0)) {
  BallPrefab newBall = Instantiate(ball);
  newBall.transform.position = transform.position;
  newBall.GetComponent<Rigidbody>().AddForce(
    Camera.main.transform.forward * Random.Range(500, 750)
  );
}
```
This will generate a ball when you touch the screen and add a random forward force. Before this will work though, we will have to connect the *BallPrefab* to the *BallShooter* script. To do this, click on the `MainCamera` in our scene and drag the BallPrefab object from the bottom of the window on to the Ball property of the `BallShooter` script. Now if you run it, you should see some plain white balls shoot out of the screen when you click. The last step is to build it on your phone see it in action!

## Grading
To get full credit for this assigment, either show me in person the app running on your phone, or record a video, then upload the project in a zip file to canvas. That's it!

## Bonus
There will be no extra credit for this assignment, but in the future I will include bonus sections at the end with an extra challenge. Here are some suggestions:
- Add extra objects in the scene and experiment with the physics engine. You can also mess with the properties of the rigidbody of our prefab and see what happens
- Make it so the balls launch from where you tap on the screen.
- Create multiple prefabs and add them to the BallShooter script, then when you tap randomly pick one
