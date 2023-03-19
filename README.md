# MongoBlogger2

A- Mongo Blogger pt2
- Create a new github repo:
- The title will be MongoBlogger
- Important: Initalize the repo WITH a README
- Clone the repo to your computer and add the link to populi
- For the assignment, you will write out your queries in NoSQLBooster and then copy/paste the final queries into the README and commit
- Copy/Paste the following code into NoSQLBooster and update the code per the comments below each function.
- Note: Feel free to update/change whatever code you need to for the CRUD functions, the important thing is that they work as intended.

//new code below

const getUUID = () => {
const max = 40
const min = 0
const randIndex = Math.floor(Math.random() * (max - min + 1) + min)
const uuidList = [
"239fc1f4-9a65-4774-afe1-c4f7626a5ad1",
"ee8ae23c-2e26-4b0b-b294-c3d0ca4850ef",
"fb1b7a41-ca45-47b5-84f7-64f27b38249b",
"a4edc658-3525-4205-9f17-c37d9c897676",
"043328c9-1e49-42c1-ac88-8177eb548b81",
"9d585fa2-4d75-43af-857c-a3111c3ad732",
"c2d455d4-a0ff-4a07-8e04-098371240003",
"81636fb8-c3b3-46b0-952f-8f5c3cf9a87d",
"25f41810-131b-40af-b163-738ea01781d4",
"15e478a8-b4dc-4433-a681-80d2c66f28e2",
"9dde5a1d-1792-43f7-b2a0-1afad837c77f",
"8b6fa098-d1cb-47ee-9d60-4dbc6b79a1c5",
"35a04237-507c-45f5-b770-3ce2c2fd088b",
"b759942f-2fcb-467e-8f25-3873d357171e",
"abcced87-72e1-46dd-b026-0b2b1e3c52bc",
"a1b3fb6e-ba2f-4614-8b4a-e7c482398982",
"09e854b1-9b78-4e01-97f7-e54cb511605a",
"92744be8-81db-4598-8693-1b2d756189a8",
"23d3563e-a211-4759-a77e-6de55d1e03ac",
"f95b8b6e-4552-4fca-a6c5-1b2588468b6e",
"e8d3df08-d1ca-41b0-a008-47754639ac98",
"53985bf3-1eec-448b-ad63-72e89baa1ea0",
"ebec6418-9540-437a-bbd0-bb552dfe2d63",
"4cc02e40-895a-442a-a58d-7956c12f535d",
"61e9e0da-2bf6-4b3b-adb2-b03326d1d7a9",
"eb4ce320-bc4f-4446-97e6-d42b6ace857f",
"f63daa0b-eb0b-47ff-91cb-cead351d87f5",
"8d850030-d5d0-47c6-8ed5-a5265c166cb4",
"68a8922a-3a69-49b5-bb2c-5cca7ecc9b8e",
"81dac8b1-06c7-40f9-94c7-ceeefa3a3475",
"afd45ade-0a6f-4a95-bdb2-5d720d1cdd25",
"5bb8d076-fa3e-4802-bbf2-f4671156a2ad",
"ad9ead68-c96d-4f7f-b246-6eb07b203743",
"07c59493-0a54-4477-8ae6-e23b01c4cb48",
"7841e93c-0bdc-4b6b-a5c4-512e280e5aa8",
"4387f4d8-aeac-4559-9f1b-3c5d537c955c",
"e365f13c-4c1d-4ee1-8a66-3dbbbab71f0d",
"08dd1f20-7d31-4120-89ed-343d4006a7cb",
"98a06f8f-50c9-4832-9d2d-daa45543db00",
"7c5d70bb-2a00-4009-9bb8-1bb163fb501f",
]
return uuidList[randIndex]
}



const searchObject = { createdAt: { $gt: new Date("2022-05-01") } };

const getPosts = (searchObject, sortObject, limit, skip) => {
  let query = db.blogs.find(searchObject);

  if (sortObject) {
    query = query.sort(sortObject);
  }

  if (limit) {
    query = query.limit(limit);
  }

  if (skip) {
    query = query.skip(skip);
  }

  const posts = query.toArray();
  return posts;
};

const createPost = (newPost) => {
  if (!newPost.title || !newPost.text || !newPost.author || !newPost.categories) {
    throw new Error("Missing required fields");
  }

  const id = getUUID();
  const createdAt = new Date();
  const lastModified = new Date();

  const postData = {
    id,
    createdAt,
    lastModified,
    ...newPost,
  };

  db.blogs.insertOne(postData);
};

const updatePost = (id, newPostData) => {
  const lastModified = new Date();
  db.blogs.updateOne({ id }, { $set: { ...newPostData, lastModified } });
};

const deletePost = (id) => {
  db.blogs.deleteOne({ id });
};

const newPost = {
  title: "The Dark Knight Movie Review",
  text: "This movie was amazing because I am Batman.",
  author: "Bruce Wayne",
  categories: ["superhero", "action", "thriller"],
};

const updatedPost = {
  title: "The Dark Knight Movie Review",
  text: "This movie was amazing because I am Batman, and totally not Bruce Wayne. I don't even know who that is.",
  author: "ALAN",
  categories: ["superhero", "action", "thriller"],
};

const postId = "53985bf3-1eec-448b-ad63-72e89baa1ea0";
const postIdToDelete = "53985bf3-1eec-448b-ad63-72e89baa1ea0";

// Uncomment the lines below one by one to test each function
// createPost(newPost)
// const posts = getPosts(searchObject, {}, 10, 0)
// console.log(posts)
// updatePost(postId, updatedPost)
deletePost(postIdToDelete)