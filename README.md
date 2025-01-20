Hey there! 👋


Build a simple drag & drop landing page builder using any of Vue.js, Angular, React. Extra points for using Vue.js.

Requirements:
Create 2 draggable blocks: Text and Image.
The content of Text block should be editable.
Image block can be edited by selecting one of the 3-4 predefined images.
The user should be able to rearrange, duplicate and delete blocks.
Landing page data like the text content, links to images, block order, etc. should be exported to a JSON format when the user clicks the “Save” button (console.log is enough).
Style the application using CSS or a CSS framework of your choice (e.g., Tailwind CSS).
The application should be responsive.
Test cases are a bonus.

Instructions:
Set up a new project.
Implement the required features based on the given requirements.
Commit your changes regularly, with clear and descriptive commit messages.
Push your final implementation to your repository.
Provide the repository URL for review.


Note: Feel free to use any additional libraries, tools, or plugins that you think would enhance the application.


Deadline: Within 5 calendar days of receiving the assignment.
Delivery: When the task is ready, please share the repository URL for review by email.


TEST CASES

1)
- Open the app
- add a new Text element
- Write: Welcome to the new MailerLite landing page builder

Expected result:
[
  {
    "id": 1,
    "type": "ContentText",
    "props": {
      "imageUrl": null,
      "imageId": 0,
      "text": "Welcome to the new MailerLite landing page builder<p></p>"
    }
  }
]


2)
- Open the app
- add a new Image element
- Choose the image with the Computer

Expected result:
[
  {
    "id": 1,
    "type": "ContentImage",
    "props": {
      "imageUrl": "/src/assets/images/image_1.jpg",
      "imageId": 1,
      "text": ""
    }
  }
]

3)
- Open the app
- Add a new Image element
- Choose the image with the Computer
- Add a new Text element
- Write: Welcome to the new MailerLite landing page builder

Expected result:
[
  {
    "id": 1,
    "type": "ContentImage",
    "props": {
      "imageUrl": "/src/assets/images/image_1.jpg",
      "imageId": 1,
      "text": ""
    }
  },
  {
    "id": 2,
    "type": "ContentText",
    "props": {
      "imageUrl": null,
      "imageId": 0,
      "text": "<p>Welcome to the new MailerLite landing page builder</p><p></p>"
    }
  }
]

4)
- Open the app
- Add a new Image element
- Choose the image with the Computer
- Add a new Text element
- Write: Welcome to the new MailerLite landing page builder
- Drag the Image to the Text Position using the Drag me button

Expected result:
[
  {
    "id": 2,
    "type": "ContentText",
    "props": {
      "imageUrl": null,
      "imageId": 0,
      "text": "<p>Welcome to the new MailerLite landing page builder</p><p></p>"
    }
  },
  {
    "id": 1,
    "type": "ContentImage",
    "props": {
      "imageUrl": "/src/assets/images/image_1.jpg",
      "imageId": 1,
      "text": ""
    }
  }
]

5)
- Open the app
- Add a new Image element
- Choose the image with the Computer
- Add a new Text element
- Write: Welcome to the new MailerLite landing page builder
- Drag the Image to the Text Position using the Drag me button
- Clone the text element
- Change the clonned element content to: Your vision, our tools – landing pages made simple. 
- Use the text editor to make it bold

Expected result:
[
  {
    "id": 3,
    "type": "ContentText",
    "props": {
      "imageUrl": null,
      "imageId": 0,
      "text": "<p>Welcome to the new MailerLite landing page builder</p><p></p>"
    }
  },
  {
    "id": 2,
    "type": "ContentText",
    "props": {
      "imageUrl": null,
      "imageId": 0,
      "text": "<p><strong>Your vision, our tools – landing pages made simple.</strong></p><p></p>"
    }
  },
  {
    "id": 1,
    "type": "ContentImage",
    "props": {
      "imageUrl": "/src/assets/images/image_1.jpg",
      "imageId": 1,
      "text": ""
    }
  }
]

6)
- Open the app
- Add a new Image element
- Choose the image with the Computer
- Add a new Text element
- Write: Welcome to the new MailerLite landing page builder
- Drag the Image to the Text Position using the Drag me button
- Clone the text element
- Change the clonned element content to: Your vision, our tools – landing pages made simple. 
- Use the text editor to make it bold
- Clone the image element
- Chose the image with the Letter

Expected result:
[
  {
    "id": 3,
    "type": "ContentText",
    "props": {
      "imageUrl": null,
      "imageId": 0,
      "text": "<p>Welcome to the new MailerLite landing page builder</p><p></p>"
    }
  },
  {
    "id": 2,
    "type": "ContentText",
    "props": {
      "imageUrl": null,
      "imageId": 0,
      "text": "<p><strong>Your vision, our tools – landing pages made simple.</strong></p><p></p>"
    }
  },
  {
    "id": 4,
    "type": "ContentImage",
    "props": {
      "imageUrl": "/src/assets/images/image_1.jpg",
      "imageId": 1,
      "text": ""
    }
  },
  {
    "id": 1,
    "type": "ContentImage",
    "props": {
      "imageUrl": "/src/assets/images/image_2.jpg",
      "imageId": 2,
      "text": ""
    }
  }
]


7)
- Open the app
- Add a new Image element
- Choose the image with the Computer
- Add a new Text element
- Write: Welcome to the new MailerLite landing page builder
- Drag the Image to the Text Position using the Drag me button
- Clone the text element
- Change the clonned element content to: Your vision, our tools – landing pages made simple. 
- Use the text editor to make it bold
- Clone the image element
- Chose the image with the Letter
- Drag the computer image to the top
- Drag the letter image to before the "Your vision, our tools – landing pages made simple." text element

Expected result:
[
  {
    "id": 4,
    "type": "ContentImage",
    "props": {
      "imageUrl": "/src/assets/images/image_1.jpg",
      "imageId": 1,
      "text": ""
    }
  },
  {
    "id": 3,
    "type": "ContentText",
    "props": {
      "imageUrl": null,
      "imageId": 0,
      "text": "<p>Welcome to the new MailerLite landing page builder</p><p></p>"
    }
  },
  {
    "id": 1,
    "type": "ContentImage",
    "props": {
      "imageUrl": "/src/assets/images/image_2.jpg",
      "imageId": 2,
      "text": ""
    }
  },
  {
    "id": 2,
    "type": "ContentText",
    "props": {
      "imageUrl": null,
      "imageId": 0,
      "text": "<p><strong>Your vision, our tools – landing pages made simple.</strong></p><p></p>"
    }
  }
]


7)
- Open the app
- Add a new Image element
- Choose the image with the Computer
- Add a new Text element
- Write: Welcome to the new MailerLite landing page builder
- Remove the image component

Expected result:
[
  {
    "id": 2,
    "type": "ContentText",
    "props": {
      "imageUrl": null,
      "imageId": 0,
      "text": "<p>Welcome to the new MailerLite landing page builder</p><p></p>"
    }
  }
]

8)
- Open the app
- Add a new Image element
- Choose the image with the Computer
- Add a new Text element
- Write: Welcome to the new MailerLite landing page builder
- Remove the text component

Expected result:
[
  {
    "id": 1,
    "type": "ContentImage",
    "props": {
      "imageUrl": "/src/assets/images/image_1.jpg",
      "imageId": 1,
      "text": ""
    }
  }
]