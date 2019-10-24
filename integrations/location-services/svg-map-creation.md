# SVG Map Creation

A full SVG Map Creation Guide can be downloaded [here](https://drive.google.com/file/d/1kET2-SLBKJJUJZK0ra7pqyX9GvCI_08_/view).

## Intro

ACA maps are where function meets form, and are the starting point of any conversation between a user and the platform.

A bespoke map is like a tailored suit or custom jewellery piece - you can elevate something simple by perfecting the details which takes the final product to the next level. The choices you make along the way will define the story you tell with the finished product. This guide will step you through the process in creating a map that is easy to use and visually effective.

When going custom you’ll get to choose from a range of details, which can really elevate your suit to the next level. Linings, button colours and stitching choices can all be made. This is much like the maps ACA designs for its clients, we take your average engineering map and we give it a makeover to impress the user.

## Step 1 - Obtain Floor Plans

Get architectural floor plan from client and branding colours \(if provided\).

![](../../.gitbook/assets/image%20%283%29.png)

## Step 2 - File Set up & Import Architecture Drawing To AI 

When working in illustrator it is important to set your artboards to pixels \(px\) for web form

* Drag drop a jpeg version of the floor plan into ai
* To get started with the right settings we need to select preferences from Illustrator&gt;preferences&gt;General
* Select "scale corners" and "scale strokes and effects" this will make sure all your objects will scale to the stroke you set it at which provides freedom in scalability .
* Select "Units" from the Side options and double check everything is set to pixels as we are working in web.

![](../../.gitbook/assets/screen-shot-2019-10-11-at-12.34.26-pm.png)

![Make sure scale corners and scale strokes and effects are selected.](../../.gitbook/assets/screen-shot-2019-10-11-at-12.35.27-pm.png)

![Select &quot;Units&quot; and double check everything is set to &quot;Pixels&quot;](../../.gitbook/assets/screen-shot-2019-10-11-at-12.36.51-pm.png)

## Step 3 - Creating Your Layers

Before getting started on design it is important to **name and order your layers**.  The ideal way to create layers is to start from the bottom working your way up. So for a floor plan that would be to start from the simple features such as the overall skeleton shaping of a building, signage such as toilets, stairs, lifts and lastly adding furniture and room statuses towards the end. 



![Original floor plan should be locked to avoid it moving out of place while designing.](../../.gitbook/assets/screen-shot-2019-10-11-at-12.51.47-pm.png)

## Step 4 - Creating Floors

In a new layer start outlining your architectural floor plan, fill in shape with colour \(as outlined by brand guidelines\), lock the layer and name layer “outline”

![](../../.gitbook/assets/image%20%2810%29.png)

## Step 5 - Floor Dimension 

Copy and paste outline and fill in with colour \(new layer\) and lock the layer - name layer “bkd”. Ensure this shape is shifted to the side or downward \(building shapes vary\) to give a shadow or building structure effect to the “outline” layer.

![](../../.gitbook/assets/image%20%281%29.png)

## Step 6 - Outlining Floors aka "The Skeleton"

It is important to note that the floor plan walls and outlines do not need the exact thickness of each wall illustrated. The plan needs to define wall areas that are entrances to spaces to rooms . The outline shape of the floor should be a little but thicker in point size compared to its inner walls to define boundaries. To get started on the skeleton -select the "pen tool" and select a point size that is best to outline walls. This can be anywhere from 2px-6px. Begin illustrating the custom map ignoring any outlines that are not needed eg pipes near bathrooms or electrical rooms can be outlined around and given a darker blank space in its fill.

![](../../.gitbook/assets/image%20%282%29.png)

## Step 7 - Space Highlights

Once rooms have been outlined check the architectural floor plan to see which spaces require signage eg rest rooms, stairs or cafe spots. these spaces can have a filled space highlight that compliments the background colour of the map.

![](../../.gitbook/assets/image%20%286%29.png)

## Step 8 - Compare Floor Plans

To make things easier check the architectural floor plan and begin placing furniture and other features in designated spaces and rooms. If you already have them designed, if not you will need to create your own according to the brand guidelines.

![](../../.gitbook/assets/image%20%2815%29.png)

## Step 9 - Completing Layers

Make sure furniture and other elements such as plants are proportional to the room size and layout. Ensure plants are kept simple and are not composed of a gradient. Once complete name layer “plants and furniture”. Once complete lock layer.

![](../../.gitbook/assets/image%20%285%29.png)

## Step 10 - Adding Bookable Rooms

In a new layer, using the “rectangle tool” begin create overlay for room bookings \(bookable rooms\), ensure the over layer is between 40%- 60% black. Room layer should be on a layer below lines \(for appearances to look neater\). Name layer “room bookings”.

![](../../.gitbook/assets/image%20%2813%29.png)

## Step 11 - Booking ID's

In this layer “room bookings” you will be required to give room ids, usually provided by the client. Clients usually give the room ids/ specification to which they would like. Capitalised or lower case, room and level number order etc... but all rooms should be labeled according to the following “area- level. room number-status”.

![](../../.gitbook/assets/image%20%288%29.png)

## Step 12 - Adding Text

Once each room layer is labeled you can create another layer “text” here you will label each room and section of the map. This text should be Arial and anything larger than 6pt text size. For rooms use Arial bold or medium for other sections of the map use Arial regular or light. Make sure text colour is white or a colour that stands out against the map background.

![](../../.gitbook/assets/image%20%2811%29.png)

## Step 13 - Adding Icons

Lastly, on another layer, add icons to your map, icons should follow the branding guidelines e.g. style, colours, line weight/thickness etc... ensure colours chosen for icons also stand out against the map background.

![](../../.gitbook/assets/image%20%289%29.png)

## Step 14 - Checking Names/ID

Once all elements are on your map go back to the booking layer and be sure to check the name and number of each room. We would recommend placing the names in order to ensure there are no double ups. Remember the SVG map will not work on the front end if two rooms have the same id.

![](../../.gitbook/assets/image.png)

## Step 15 - Exporting

Go to file&gt;export as&gt;SVG&gt; save to designated folder &gt; ensure the following is correct:  
styling &gt; internal CSS  
Font &gt; SVG

Images &gt; preserve  
Object IDs&gt; Layer names Decimal &gt; 3  
Tick &gt; minify and responsive Select &gt; ok

![](../../.gitbook/assets/image%20%2814%29.png)

## Checklist

* [ ] Client Architectural floor plans
* [ ] Client room ids and room names
* [ ] Client/brand guidelines
* [ ] client/brand colour pallet
* [ ] create furniture and plants that follow client/brand guidelines
* [ ] Have the latest Adobe Illustrator CC2019
* [ ] Name the file "client\_map\_level"
* [ ] Name layers
* [ ] Save As.. \(Always\)
* [ ] Once you complete check room ids for no duplicates

