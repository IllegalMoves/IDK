# IDK
6var board,
  game = new Chess();

// do not pick up pieces if the game is over
// only pick up pieces for White
var onDragStart = function(source, piece, position, orientation) {
  if (game.in_checkmate() === true || game.in_draw() === true ||
    piece.search(/^b/) !== -1) {
    return false;
  }
};

var makeRandomMove = function() {
  var possibleMoves = game.moves();

  // game over
  if (possibleMoves.length === 0) return;

  var randomIndex = Math.floor(Math.random() * possibleMoves.length);
  game.move(possibleMoves[randomIndex]);
  board.position(game.fen());
};

var onDrop = function(source, target) {
  // see if t};
board = ChessBoard('board', cfg);
HTML
<script src="js/chess.js"></script>
<div id="board" style="width: 400px"></div>
var board,
  game = new Chess();

// do not pick up pieces if the game is over
// only pick up pieces for White
var onDragStart = function(source, piece, position, orientation) {
  if (game.in_checkmate() === true || game.in_draw() === true ||
    piece.search(/^b/) !== -1) {
    return false;
  }
};

var makeRandomMove = function() {
  var possibleMoves = game.moves();

  // game over
  if (possibleMoves.length === 0) return;

  var randomIndex = Math.floor(Math.random() * possibleMoves.length);
  game.move(possibleMoves[randomIndex]);
  board.position(game.fen());
};

var onDrop = function(source, target) {
  // see if the move is legal
  var move = game.move({
    from: source,
    to: target,
    promotion: 'q' // NOTE: always promote to a queen for example simplicity
  });

  // illegal move
  if (move === null) return 'snapback';

  // make random legal move for black
  window.setTimeout(makeRandomMove, 250);
};

// update the board position after the piece snap
// for castling, en passant, pawn promotion
var onSnapEnd = function() {
  board.position(game.fen());
};

var cfg = {
he move is legal
  var move = game.move({
    from: source,
    to: target,
    promotion: 'q' // NOTE: always promote to a queen for example simplicity
  });

  // illegal move
  if (move === null) return 'snapback';

  // make random legal move for black
  window.setTimeout(makeRandomMove, 250);
};

// update the board position after the piece snap
// for castling, en passant, pawn promotion
var onSnapEnd = function() {
  board.position(game.fen());
};

var cfg = {
  draggable: true,
  position: 'start',
  onDragStart: onDragStart,
  onDrop: onDrop,
  onSnapEnd: onSnapEnd
};
board = ChessBoard('board', cfg);
HTML
<script src="js/chess.js"></script>
<div id="board" style="width: 400px"></div>
var board,
  game = new Chess();

// do not pick up pieces if the game is over
// only pick up pieces for White
var onDragStart = function(source, piece, position, orientation) {
  if (game.in_checkmate() === true || game.in_draw() === true ||
    piece.search(/^b/) !== -1) {
    return false;
  }
};

var makeRandomMove = function() {
  var possibleMoves = game.moves();

  // game over
  if (possibleMoves.length === 0) return;

  var randomIndex = Math.floor(Math.random() * possibleMoves.length);
  game.move(possibleMoves[randomIndex]);
  board.position(game.fen());
};

var onDrop = function(source, target) {
  // see if the move is legal
  var move = game.move({
    from: source,
    to: target,
    promotion: 'q' // NOTE: always promote to a queen for example simplicity
  });

  // illegal move
  if (move === null) return 'snapback';

  // make random legal move for black
  window.setTimeout(makeRandomMove, 250);
};

// update the board position after the piece snap
// for castling, en passant, pawn promotion
var onSnapEnd = function() {
  board.position(game.fen());
};

var cfg = {
  draggable: true,
  position: 'start',
  onDragStart: onDragStart,
  onDrop: onDrop,
  onSnapEnd: onSnapEnd
};
board = ChessBoard('board', cfg);

var evaluateBoard = function(board, color) {




 // Sets the value for each piece using standard piece value


 var pieceValue = {


   'p': 100,


   'n': 350,


   'b': 350,


   'r': 525,


   'q': 1000,


   'k': 10000


 };







 // Loop through all pieces on the board and sum up total


 var value = 0;


 board.forEach(function(row) {


   row.forEach(function(piece) {


     if (piece) {


       // Subtract piece value if it is opponent's piece


       value += pieceValue[piece['type']]


                * (piece['color'] === color ? 1 : -1);


     }


   });


 });







 return value;


};

var calcBestMoveOne = function(playerColor) {




 // List all possible moves


 var possibleMoves = game.moves();


 // Sort moves randomly, so the same move isn't always picked on ties


 possibleMoves.sort(function(a, b){return 0.5 - Math.random()});







 // exit if the game is over


 if (game.game_over() === true || possibleMoves.length === 0) return;







 // Search for move with highest value


 var bestMoveSoFar = null;


 var bestMoveValue = Number.NEGATIVE_INFINITY;


 possibleMoves.forEach(function(move) {


   game.move(move);


   var moveValue = evaluateBoard(game.board(), playerColor);


   if (moveValue > bestMoveValue) {


     bestMoveSoFar = move;


     bestMoveValue = moveValue;


   }


   game.undo();


 });







 return bestMoveSoFar;


}

var calcBestMoveNoAB = function(depth, game, playerColor,




                               isMaximizingPlayer=true) {


 // Base case: evaluate board


 if (depth === 0) {


   value = evaluateBoard(game.board(), playerColor);


   return [value, null]


 }






 var bestMove = null; // best move not set yet
 var possibleMov
var calcBestMoveNoAB = function(depth, game, playerColor,




                               isMaximizingPlayer=true) {


 // Base case: evaluate board


 if (depth === 0) {


   value = evaluateBoard(game.board(), playerColor);


   return [value, null]


 }





es = game.moves();
 // Set random order for possible moves

 possibleMoves.sort(function(a, b){return 0.5 - Math.random()});
 // Set a default best move value
 var bestMoveValue = isMaximizingPlayer ? Number.NEGATIVE_INFINITY
                                        : Number.POSITIVE_INFINITY;
 // Search through all possible moves
 for (var i = 0; i < possibleMoves.length; i++) {
   var move = possibleMoves[i];
   // Make the move, but undo before exiting loop
   game.move(move);
   // Recursively get the value of this move
   value = calcBestMoveNoAB(depth-1, game, playerColor, !isMaximizingPlayer)[0];
   // Log the value of this move
   console.log(isMaximizingPlayer ? 'Max: ' : 'Min: ', depth, move, value,
               bestMove, bestMoveValue);



   if (isMaximizingPlayer) {
     // Look for moves that maximize position
     if (value > bestMoveValue) {
       bestMoveValue = value;
       bestMove = move;
     }
   } else {



































 // Recursive case: search possible moves


 var bestMove = null; // best move not set yet


 var possibleMov
var calcBestMoveNoAB = function(depth, game, playerColor,




                               isMaximizingPlayer=true) {


 // Base case: evaluate board


 if (depth === 0) {


   value = evaluateBoard(game.board(), playerColor);


   return [value, null]


 }





es = game.moves();


 // Set random order for possible moves


 possibleMoves.sort(function(a, b){return 0.5 - Math.random()});


 // Set a default best move value


 var bestMoveValue = isMaximizingPlayer ? Number.NEGATIVE_INFINITY


                                        : Number.POSITIVE_INFINITY;


 // Search through all possible moves


 for (var i = 0; i < possibleMoves.length; i++) {


   var move = possibleMoves[i];


   // Make the move, but undo before exiting loop


   game.move(move);


   // Recursively get the value of this move


   value = calcBestMoveNoAB(depth-1, game, playerColor, !isMaximizingPlayer)[0];


   // Log the value of this move


   console.log(isMaximizingPlayer ? 'Max: ' : 'Min: ', depth, move, value,


               bestMove, bestMoveValue);







   if (isMaximizingPlayer) {


     // Look for moves that maximize position


     if (value > bestMoveValue) {


       bestMoveValue = value;


       bestMove = move;


     }


   } else {


     // Look for moves that minimize position


     if (value < bestMoveValue) {


       bestMoveValue = value;


       bestMove = move;


     }


   }


   // Undo previous move


   game.undo();


 }


 // Log the best move at the current depth


 console.log('Depth: ' + depth + ' | Best Move: ' + bestMove + ' | ' + bestMoveValue);


 // Return the best move, or the only move


 return [bestMoveValue, bestMove || possibleMoves[0]];

