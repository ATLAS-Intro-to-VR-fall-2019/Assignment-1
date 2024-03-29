# Intro To VR: Assignment 1

## Goals
- Get course development environement setup
- Build Familiarity with Unity Concepts
- Iron out the kinks of mobile deployment

## Setup
Download and install [Unity Hub](https://unity3d.com/get-unity/download), this will let you install multiple Unity versions and manage your projects. You will have to make a free Unity account before you can start developing.

Once you have your basic environment setup, create a new project with Unity Hub. Hit the big blue **NEW** button in the upper right, make sure **3D** is selected on your left, then give your project an appropriate name and location on your computer.

## Creating a Simple Scene
Click on your project in Unity Hub to open it. If you have never used Unity before, take a moment to familiarize yourself with the editor once Unity boots up. Here are some resources that might help you get acquainted.
- [Basic Interface Overview](https://docs.unity3d.com/Manual/LearningtheInterface.html)
- [Interface Overview Video](https://www.youtube.com/watch?v=D7v2pjke5sc)
- [GameObjects and Components Video](https://www.youtube.com/watch?v=9Nf2_ds5y8c)
- [About an Hour of Interface Overviews](https://learn.unity.com/tutorial/using-the-unity-interface?courseId=5c8bcd60edbc2a0020e41e6d#)

[The Unity Manual](https://docs.unity3d.com/Manual/index.html) is also a pretty detailed resource.

### Examining the Sample Scene
When you create and open a new project, it should automatically open a sample scene. A **Scene** is essentially a user defined setup for a specific part of the application. For these first few assignments we will be using only one scene, but let's rename *SampleScene* to *Main* by right clicking it in the project area at the bottom of the window and selecting rename. We are calling it *Main* because it's the main part (the only one in this case) of our application.

If you look to the left of the screen, you should see the **Heirarchy** window. There you should see two objects: Main Camera, and Directional Light. Unity refers to these objects as **GameObjects** and they can do a lot. If you click on `Main Camera` you should see a camera view cone appear in the *Scene* window in the middle of the screen, and the inspector on the right side of the screen, the **Inspector**, will change to show what *components* are attached to it. **Components** are what contain all of the functionality in Unity, each GameObject will always have a *Transform* component, which is used to set and display the position, rotation, and scale of a GameObject. You may also notice other components attached to the Main Camera, these tell the game engine that this GameObject is a camera.

### Let's Add Our Own Object
Right click in the Heirarchy and select `3D Object -> Sphere`, you should see a sphere appear in the middle of the Scene view and in the Heirarchy a new GameObject called `Sphere`. Let's rename Sphere to `Ball`. You can edit the transform of the ball by either moving it manually in the scene editor or changing the `transform` values in the Inspector. If you move it by had, pay attention to the `transform` component and see the values change.

Finally, let's create our own component. Select the Ball in the Heirarchy and in the Inspector and click the `Add Component` button at the bottom. Select the new script option, and add a script named `BallPrefab`. If you select this script in the Project window, it will open the IDE that Unity comes with and show you a generated file template. For now we won't be editing this, and I will cover the default script in class next week. We will be using this script as a reference in a later part of the assignment. First let's try and get it running on your phones.

## Deploying
Now that you have an scene to deploy, let's get you set up to run it on your phone. First close Unity since we will be adding new libraries. Follow the setup guide for the type of phone you have. You can add moduals to your Unity installation by going to the **Installs** tab in Unity Hub, and clicking on the 3 dots on the version you are using, then selecting **Add Modules**. When following these tutorials, skip past their scene setup and go straight to the deploying section.
- [Android](https://docs.unity3d.com/Manual/android-sdksetup.html)
- [IOS](https://learn.unity.com/tutorial/building-for-mobile#5c7f8528edbc2a002053b4a1)

## Let's Make it Interactive!
We are going to make it so that when you tap the screen, a ball shoots out from the center. First we will have to make a **Prefab** for the ball. Prefabs are templates for objects that we can create at runtime, they make it easy to create a lot of really similar objects. To turn the ball into a prefab, simply drag it into the project area at the bottom of the window next to the scenes folder.

Select the Ball from the Project window and you should see it show up on the right side of the inspector. From here we can edit our default values for all future instances of the prefab. For now, just add the **Rigidbody** component to give our ball physics.

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
This will generate a ball when you touch the screen and add a random forward force. Before this will work though, we will have to connect the *BallPrefab* to the *BallShooter* script. To do this, click on the `MainCamera` in our scene and drag the Ball prefab object from the bottom of the window on to the Ball property of the *BallShooter* script. Now if you run it, you should see some plain white balls shoot out of the screen when you click. The last step is to build it on your phone see it in action!

## Grading
To get full credit for this assigment, either show me in person the app running on your phone, or record a video, then upload the project in a zip file to canvas. That's it!

## Bonus
There will be no extra credit for this assignment, but in the future I will include bonus sections at the end with an extra challenge. Here are some suggestions:
- Add extra objects in the scene and experiment with the physics engine. You can also mess with the properties of the rigidbody of our prefab and see what happens
- Make it so the balls launch from where you tap on the screen.
- Create multiple prefabs and add them to the BallShooter script, then when you tap randomly pick one
