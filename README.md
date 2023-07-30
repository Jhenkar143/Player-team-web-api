# Player-team-web-api
Designing a code for player team
// Import the necessary modules.
const express = require("express");
const mongoose = require("mongoose");
// Create a new Express application.
const app = express();
// Connect to the database.
mongoose.connect("mongodb://localhost/players");
// Define the API routes.
app.get("/players", (req, res) => {
  // Get all of the players from the database.
  const players = mongoose.model("Player").find();
  // Return the players to the client.
  res.send(players);
});
app.post("/players", (req, res) => {
  // Create a new player from the request body.
  const player = new mongoose.model("Player", req.body);
  // Save the player to the database.
  player.save((err, player) => {
    if (err) {
      res.send(err);
    } else {
      res.send(player);
    }
  });
});
app.put("/players/:id", (req, res) => {
  // Get the player from the database.
  const player = mongoose.model("Player").findById(req.params.id);
  // Update the player with the request body.
  player.name = req.body.name;
  player.position = req.body.position;
  player.skills = req.body.skills;
  // Save the player to the database.
  player.save((err, player) => {
    if (err) {
      res.send(err);
    } else {
      res.send(player);
    }
  });
});
app.delete("/players/:id", (req, res) => {
  // Get the player from the database.
  const player = mongoose.model("Player").findById(req.params.id);
  // Delete the player from the database.
  player.remove((err, player) => {
    if (err) {
      res.send(err);
