import maya.cmds as cmds

# create UI 
                
if 'UI' in globals():
    if cmds.window(UI, exists=True):
        cmds.deleteUI(UI, window=True)     
                          
UI = cmds.window(title='Scripting', width=400)

cmds.columnLayout(rowSpacing=10)

cmds.text(label='Scripting')
                
cmds.intSliderGrp('width', label='width',min=1, max=5)
cmds.intSliderGrp('height', label='Height',min=1, max=5)
cmds.intSliderGrp('depth', label='Depth',min=1, max=5)
                
cmds.checkBox('includeChimney', label='include Chimney')
cmds.checkBox('includeWindows', label='include Windows')
                
                                
cmds.button(label='Generate House', command= 'generateHouse()')
                
                                
cmds.button(label='Generate Random House', command= 'generateRandomHouse()')
                
                                
cmds.showWindow(UI)

# Functions 
                
def generateChimney(dimensions):       
    chimney = cmds.polyCube(width=0.2, height=1.0, depth=0.2)     
    cmds.move(dimensions[0] / 3.0, dimensions[1] + 0.2 , dimensions[2] / 3.0)
        
    return chimney 

def generateWindowPrimitive():
    A = cmds.polyCube(width=0.1, height=0.1, depth= 0.1)     
    cmds.move(0.1,0,0)
        
    B = cmds.polyCube(width=0.1, height=0.1, depth= 0.1)     
    cmds.move(-0.1,0,0)   
    
    C = cmds.polyCube(width=0.1, height=0.1, depth= 0.1)     
    cmds.move(0.1,0.2,0)  
    
    D = cmds.polyCube(width=0.1, height=0.1, depth= 0.1)     
    cmds.move(-0.1,0.2,0)    
    cmds.select(A, B, C, D)
    windowPrimitives = cmds.polyUnite()
    cmds.move(0, 0.2, 0.5)     
        
    return windowPrimitives
               
def generateWindows(dimensions, wallSet):
    
    windowObject = generateWindowPrimitive()
    
    cmds.polyCBoolOp(wallSet, windowObject[0], op=2)

        
    generateWindowPrimitive()      
    # Generate from incoming parameters
        
def generateParametricHouse(houseWidth, houseHeight, houseDepth):
    # Generate from incoming parameters
        
    #createbase       
    base = cmds.polyCube( width= houseWidth, height = 0.1, depth=houseDepth)
                        
    # Create walls
    WallA = cmds.polyCube( width= 0.05, height = houseHeight, depth=houseDepth) 
    cmds.move(houseWidth/2.0,houseHeight/2.0,0) 
    #B        
    WallB = cmds.polyCube( width= 0.05, height = houseHeight, depth=houseDepth) 
    cmds.move(houseWidth/-2.0,houseHeight/2.0,0)  
    #C
    WallC = cmds.polyCube( width= houseWidth, height = houseHeight, depth=0.05) 
    cmds.move(0, houseHeight/2, houseDepth/2)       
    #D     
    WallD = cmds.polyCube( width= houseWidth, height = houseHeight, depth=0.05) 
    cmds.move(0, houseHeight/2, houseDepth/-2)   
                  
    cmds.select(WallA, WallB, WallC, WallD)
    wallSet= cmds.polyUnite()                                   
        
    #Creating the Roof
    roof = cmds.polyCube( width= houseWidth, height = 0.35, depth= houseDepth)
    cmds.scale(1.2,1.2,1.2)
    cmds.move(0, houseHeight + 0.2, 0)
    cmds.select(roof[0] + '.f[1]')
    cmds.polyBevel(offset=0.3)  
                             
    #Create Chimney
    chimney = []
                
    if (cmds.checkBox('includeChimney', query=True, value=True)== True ):
        chimney = generateChimney([houseWidth, houseHeight, houseDepth])
    
    # Create windows
    if (cmds.checkBox('includeWindows', query=True, value=True)== True ):
        wallSet = generateWindows([houseWidth, houseHeight, houseDepth], wallSet)
                                              
def generateHouse():
    #generate the parametric house
    houseWidth = cmds.intSliderGrp('width', query=True, value=True)
    houseHeight = cmds.intSliderGrp('height', query=True, value=True) 
    houseDepth = cmds.intSliderGrp('depth', query=True, value=True) 
                        
    generateParametricHouse(houseWidth, houseHeight, houseDepth)
#def generateRandomHouse():   
#generate the random parametric house
