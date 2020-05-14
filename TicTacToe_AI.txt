# -*- coding: utf-8 -*-
"""
Created on Wed May 13 13:29:16 2020

@author: D.YOKESH
"""

import time
import os
import random

#The list containing the current status of board (1x10 - first space is left unused)
board=[""," "," "," "," "," "," "," "," "," "]

print("The following are the board indices")
print("   |   |   ")
print(" 1 | 2 | 3 ")
print("   |   |   ")
print("---|---|---")
print("   |   |   ")
print(" 4 | 5 | 6 ")
print("   |   |   ")
print("---|---|---")
print("   |   |   ")
print(" 7 | 8 | 9 \n")
print("Type the respective index number to place X/O\n")

#Define the print_board function
def printBoard():
    print("   |   |   ")
    print(" "+board[1]+" | "+board[2]+" | "+board[3]+"  ")
    print("   |   |   ")
    print("---|---|---")
    print("   |   |   ")
    print(" "+board[4]+" | "+board[5]+" | "+board[6]+"  ")
    print("   |   |   ")
    print("---|---|---")
    print("   |   |   ")
    print(" "+board[7]+" | "+board[8]+" | "+board[9]+"  ")
    
def isWinner(board, player):
    if  (board[1]==player and board[2]==player and board[3]==player) or\
        (board[4]==player and board[5]==player and board[6]==player) or\
        (board[7]==player and board[8]==player and board[9]==player) or\
        (board[1]==player and board[4]==player and board[7]==player) or\
        (board[2]==player and board[5]==player and board[8]==player) or\
        (board[3]==player and board[6]==player and board[9]==player) or\
        (board[1]==player and board[5]==player and board[9]==player) or\
        (board[3]==player and board[5]==player and board[7]==player): 
            return True
    return False

def isBoardFull(board):
    isFull = True
    if " " in board: isFull=False
    return isFull

def getComputerInput(board, player):
    
    #if center space is empty, fill that first
    if board[5]==" ":   return 5
    
    #To find opposite players symbol
    symbols=['X','O']
    
    #Check the possibilty of opposition player to win and fill that box first
    if player==symbols[0]:  
        opposite_player=symbols[1]
    else:                   
        opposite_player=symbols[0]
        
    for i in range(1,10):
        if board[i] == " ":
            board[i]=opposite_player
            if isWinner(board, opposite_player):
                return i
            else:
                board[i]=" "
                
    #Else Chech our possibility of winning and fill that box
    for i in range(1,10):
        if board[i] == " ":
            board[i]=player
            if isWinner(board, player):
                return i
            else:
                board[i]=" "                
            
    #if both are not possible, fill the spaces randomly     
        while True:
            choice = random.randint(1,9)
            if(board[choice]==" "):
                return choice
    
#Getting input from user and storing it in the List board
while True:
    os.system("clear")
    printBoard()
    
    choice = input("Please choose an empty space in the board: ")
    if choice not in ['1','2','3','4','5','6','7','8','9']:
        print("Give valid input")
        continue;
    else:
        choice=int(choice)
    
    if board[choice]==" ":
        board[choice]="X"
    else:
        print("The position is already filled")
        time.sleep(1)
        continue
    
    #Check whether X wins
    if isWinner(board,"X"):
        os.system("clear")
        printBoard()
        print("X won, congrajulations!!!")
        break;
    
    #Check for Tie   
    if isBoardFull(board):
        os.system("clear")
        printBoard()
        print("\n***Game Tied***")
        break
    
    # Get input from O:
    board[getComputerInput(board, "O")]="O"
    os.system("clear")
    
    #Check whether X wins
    if isWinner(board,"O"):
        os.system("clear")
        printBoard()
        print("O won, congrajulations!!!")
        break;
        
    #Check for Tie    
    if isBoardFull(board):
        os.system('clear')
        printBoard()
        print("\n***Game Tied***")
        break
