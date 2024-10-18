<script lang="ts">
	import ProjectCard from '$lib/components/ui/projectcard/projectcard.svelte';
	import * as Card from '$lib/components/ui/card/index';
	import * as Carousel from '$lib/components/ui/carousel/index.js';
	import Proximityglow from '$lib/components/ui/proximityglow/proximityglow.svelte';
	import { Separator } from '$lib/components/ui/separator';
	import Scrambletext from '$lib/components/ui/scrambletext/scrambletext.svelte';
	import Typetext from '$lib/components/ui/typetext/typetext.svelte';
	import Woah from '$lib/components/ui/typetext/woah.svelte';
	import * as Accordion from '$lib/components/ui/accordion';
	import Projectcard from '$lib/components/ui/projectcard/projectcard.svelte';
	import { AspectRatio } from '$lib/components/ui/aspect-ratio';

	let ckeyFeatures = [
		{
			group: [
				{
					title: 'Feature 1',
					description: 'Description 1',
					gifPath: 'https://i.postimg.cc/44qS12hK/search.gif'
				},
				{
					title: 'Feature 2',
					description: 'Description 2',
					gifPath: 'https://i.postimg.cc/QM84MRvz/titlepage.gif'
				},
				{
					title: 'Feature 3',
					description: 'Description 3',
					gifPath: 'https://i.postimg.cc/sDW0HPpT/mangareview.gif'
				}
			],

			title: 'Features 1'
		},
		{
			group: [
				{
					title: 'Feature 4',
					description: 'Description 4',
					gifPath: 'https://i.postimg.cc/3Nv4Cq5C/chapterpage.gif'
				},
				{
					title: 'Feature 5',
					description: 'Description 5',
					gifPath: 'https://i.postimg.cc/htqZkJsc/chapterreview.gif'
				},
				{
					title: 'Feature 6',
					description: 'Description 5',
					gifPath: 'https://i.postimg.cc/L4nWLFhK/login.gif'
				}
			],
			title: 'Features 2'
		},
		{
			group: [
				{
					title: 'Feature 7',
					description: 'Description 5',
					gifPath: 'https://i.postimg.cc/5jWHPmfc/like.gif'
				},
				{
					title: 'Feature 8',
					description: 'Description 5',
					gifPath: 'https://i.postimg.cc/3NmC1BPp/profile.gif'
				}
			],
			title: 'Features 3'
		}
	];
	let projects = [
		{
			title: 'Current: Anichapter',
			overview:
				'Anichapter is a manga and chapter rating website aiming to provide a platform to rate individual chapters of manga similar to how movies are rated on IMDB. It is developed with a focus on simplicity. The website domain name has already been registered at anichapter.com.',
			videoPath: '',
			keyFeatures: [
				{
					title: 'Main Page',
					description:
						'The landing page consists of a single search bar, with animation upon mouse click. It is entirely unpopulated until the user presses enter. The search bar itself shows the top 5 results before the user clicks enter or search. The logo was made by me. The plans for the future was to have this act also as a "hot" page, where the user can see top manga, top chapters, top reviews for either, and top friend reviews. This is already semi implemented in the database, although only with top manga.',
					gifPaths: ['https://i.postimg.cc/44qS12hK/search.gif'],
					orientation: 'gif-desc'
				},
				{
					title: 'Search',
					description:
						'All images would be hosted on some image hosting service, which is undecided right now. All manga titles, as well any other data needed to be stored is stored and fetched using MongoDB. This the main database has a collection for chapter reviews, chapters, the discover page, which updates periodically, mangaReviews, mangas and users. This was done because I did not want to use SQL. For dev testing, the mangas and their details such as number of chapters were fetched from manga pirating sites. ',
					gifPaths: ['https://i.postimg.cc/QM84MRvz/titlepage.gif'],
					orientation: 'desc-gif'
				},
				{
					title: 'Title Page',
					description:
						'On the title page, the user can review the manga by clicking on the review button. This is currently unimplemented although the base work for submitting a review with token authorisation and checking is already done in the backend. There is currently no filtering, but the user can add 3 main genres that the manga fits for. This separates this site from other review sites, as all data is decided upon group voting.',
					gifPaths: ['https://i.postimg.cc/sDW0HPpT/mangareview.gif'],
					orientation: 'gif-desc'
				},
				{
					title: 'Chapter Dialog',
					description:
						'There is also a list of chapters for each manga. The user can click on each chapter/ load more, and review each. The dialog that comes upon a click displays a card reflecting the chapter score, misc data, a carousel of the top, hot, and friend review. This feature is already implemented. The top user can also dummy review the chapter with a cool custom implementation. The chapters are currently unnamed, as there aren<q>t any easy sources for such information.',
					gifPaths: ['https://i.postimg.cc/3Nv4Cq5C/chapterpage.gif'],
					orientation: 'desc-gif'
				},
				{
					title: 'Reviews Page',
					description:
						'Each manga and each chapter has a number of fake dummy reviews generated from fake dummy users. These users are mass generated when running the backend for the first time, of course, these users truly exist on the database, as well as all their reviews. The user can like the review is logged in, if not, they will be redirected to a functioning login page. The likes are correctly stored and remembered by the website. The user can see all reviews for the manga. Currently unfiltered and unsorted. There the user can also see top users by likes.',
					gifPaths: ['https://i.postimg.cc/htqZkJsc/chapterreview.gif'],
					orientation: 'gif-desc-row'
				},
				{
					title: 'Loign/Register',
					description:
						'The user can login, which is ready implemented with a generated JWC token. The user can also register on the database. The passwords are of-course hashed. Funny fact is that right now, no matter where a user<q>s data is requested, the entire unfiltered user data is given, including the hashed password. Currently, the user token is timed for 1 hour, when it refreshes. For now, the token is simply stored in the local storage.',
					gifPaths: ['https://i.postimg.cc/L4nWLFhK/login.gif'],
					orientation: 'desc-gif'
				},
				{
					title: 'Profile Page',
					description:
						'Users have profile pages, which show their followers, following, their chapter and manga reviews separated, with a function to see all reviews of the user. The user can also follow the other user, and the data will update accordingly. (weirdly a pain to do). For now, this website is locked into manga, which would need to be manually updated for relevance in terms of chapter count and name, however, later, I can see making this automatic.',
					gifPaths: ['https://i.postimg.cc/3NmC1BPp/profile.gif'],
					orientation: 'gif-desc-row'
				}
			],
			thumbnail: 'https://i.postimg.cc/2yKFT4B2/Screenshot-2024-10-04-011044.png',
			note: 'This is a project is currently in the works and is planned to be released as a real website.',
			noteColor: '#5c1c2c',
			isSpecial: 'no'
		},
		{
			title: '2024 - Terrain Layout Generator',
			overview:
				'The project was developed to address the need for automating the creation of large-scale, balanced, and varied 3D terrain maps in video games, specifically focusing on the challenges associated with manual content production in the gaming industry',
			videoPath: '',
			keyFeatures: [
				{
					title: 'Feature 1',
					description: 'Description 1',
					gifPaths: [
						'https://i.postimg.cc/m2WJCrbT/UI.gif',
						'https://i.postimg.cc/nrBWgy18/Drawing.gif',
						'https://i.postimg.cc/B68kcLLn/Adding-a-new-spot.gif',
						'https://i.postimg.cc/59CDXzWP/Settings.gif'
					],
					orientation: 'gif-desc'
				},
				{
					title: 'UI',
					description:
						'In the process of the project development, it was recognised that an easy to implement UI will serve greatly in keeping with the project feature deadlines set. This meant a robust and easy UI. For this was developed a sort of UI engine or framework, where the programmer could quickly create UI using code. The WindowManager class in this context functions as a management system for creating and controlling a user interface window within the application. Alongside the WindowManager class, there are abstract and derived component classes. Layout Mapping will be the original editing stage where the user can define areas of gameplay. This includes allowing the user to select spots, edit spot brush size, edit the spot’s position, add new spots, and remove spots.',
					gifPaths: [],
					orientation: 'desc-gif'
				},
				{
					title: 'Gen Pictures1',
					description: 'Description 1',
					gifPaths: [
						'https://i.postimg.cc/43VJYt9C/Screenshot-2024-04-09-004138.png',
						'https://i.postimg.cc/RZ3Cz2CZ/Screenshot-2024-04-09-004200.png'
					]
				},
				{
					title: 'Generation',
					description:
						'This project generates procedural islands using Perlin and Voronoi noise. Users select grid cells to initialize Perlin noise spots, which are normalized using a square bump function and positioned on the grid. The resolution can be lowered to simulate a map-like structure. Voronoi noise defines height areas by generating and colouring points based on proximity, and wave function collapse (WFC) is used for segmenting tiles into 9-cell squares. Architectural features like ramps, ceilings, slopes, and parapets are added to for usability and realism and are called the spice, with ramps being most important within said spice to ensure transitions between different elevations.',
					gifPaths: [],
					orientation: 'gif-desc'
				},
				{
					title: 'Gen Pictures2',
					description: 'Description 1',
					gifPaths: [
						'https://i.postimg.cc/DZh7LZrS/Screenshot-2024-04-09-003646.png',
						'https://i.postimg.cc/nchc3C67/Screenshot-2024-04-09-011438.png'
					],
					orientation: 'gif-desc'
				},
				{
					title: 'Animation',
					description: 'There is also a nice animation :)',
					gifPaths: ['https://i.postimg.cc/ZqsXdFqQ/Generating.gif'],
					orientation: 'gif-desc'
				},
				{
					title: 'Pics',
					description: 'Description 1',
					gifPaths: [
						'https://i.postimg.cc/zBk8jr70/Screenshot-2024-04-09-002809.png',
						'https://i.postimg.cc/sgtjfK19/Screenshot-2024-04-09-002820.png'
					],
					orientation: 'gif-desc'
				},
				{
					title: 'Routing',
					description:
						'Wave Function Collapse (WFC) was used to set up the main routing system at the first height level of the generated map, making sure all locations are connected. Local areas and continents are defined by grouping voxels at the same height level. If these groups are connected, they form a continent, each labelled with a unique index. Continents are then split into local areas, each with its own local and global index. Routing links these local areas, with some randomness deciding if paths are created between areas on the same continent. Connections are made by finding adjacent areas, figuring out paths through walls or barriers with adjacency rules, and generating pathways or mazes to link them. The script includes helper functions to clean and merge grids, spot walls, and pick entrance points, adding a bit of randomness when deciding between maze or path generation for the connections.',
					gifPaths: [],
					orientation: 'desc-gif'
				},
				{
					title: 'Feature 6',
					description: 'Description 6',
					gifPaths: [
						'https://i.postimg.cc/8c1PQ5c2/Screenshot-2024-04-09-031657.png',
						'https://i.postimg.cc/9MPFnTmP/Screenshot-2024-04-09-031721.png',
						'https://i.postimg.cc/59325wkb/Screenshot-2024-04-09-011303.png',
						'https://i.postimg.cc/8PXk9TSY/Screenshot-2024-04-09-011259.png',
						'https://i.postimg.cc/sXt8nj79/Exploring.gif'
					],
					orientation: 'desc-gif'
				}
			],
			thumbnail: 'https://i.postimg.cc/kG4LKctC/thumb.png',
			engine: 'Unity',
			note: '',
			noteColor: '#ff0266',
			isSpecial: 'no'
		},
		{
			title: '2023/24 - WFC Horror Implementation',
			overview:
				'This is a Player and Card Generator for a Potential Team Management Tycoon Game, also has manual UI integration in GML.',
			videoPath: '',
			keyFeatures: [
				{
					title: 'Nice UI',
					description:
						'The project features a nice UI I really enjoyed making and like to show off, considering I have no real design experience.',
					gifPaths: ['https://i.postimg.cc/c1hwM9W6/menu.gif'],
					orientation: 'gif-desc'
				},
				{
					title: 'Generation',
					description:
						'The Wave Function Collapse (WFC) algorithm is broken into three main steps: selecting a cell with the lowest entropy, collapsing that cell, and propagating constraints across the grid. Entropy refers to the number of possible tiles for a cell; the cell with the fewest options is chosen first. Initially, entropy is equal for all cells, so a random cell is selected. The method "FindLowestEntropyCell" finds the cell to collapse by checking the cells and identifying the one with the lowest entropy value.',
					gifPaths: ['https://i.postimg.cc/PJSDXxy1/generation.gif'],
					orientation: 'desc-gif'
				},
				{
					title: 'Steps',
					description:
						'Collapsing a cell means choosing a random tile from its possible options and assigning it to that cell. To prevent contradictions, a "Null" tile is used, which can connect with anything except empty space. The "SelectTile" method handles this by removing the "Null" tile before selecting from the remaining options. Propagation uses a queue to spread the constraints from the collapsed cell to its neighbours. The neighbours are updated based on the overlap rules, which define valid tiles in adjacent positions. If the neighbour<q>s possible tiles change, the neighbour is added to the queue, and the process continues until all constraints are updated. This ensures consistency across the entire grid.',
					gifPaths: [],
					orientation: 'desc-gif'
				},
				{
					title: 'Pics',
					description: 'Description 1',
					gifPaths: [
						'https://i.postimg.cc/26Qy4MNQ/Screenshot-2023-12-09-083917.png',
						'https://i.postimg.cc/k43DR9zM/Screenshot-2023-12-09-085740.png'
					],
					orientation: 'gif-desc'
				},
				{
					title: 'Implementation',
					description:
						'Rules for tile connections are stored in a dictionary, with each tile type linked to a set of direction-specific connection rules. The WFCManager script oversees grid initialization and the application of these rules. It also runs a check to identify isolated regions, ensuring only the largest region is kept, and handles player, enemy, and NavMesh instantiation. Originally, tiles were represented by 3x3 cube grids to create T, L, and BOX shapes, but these were later replaced with hallway models made in Blender. This change led to some challenges with NavMesh, edge tiles, and lighting.',
					gifPaths: ['https://i.postimg.cc/Wzs3S8sQ/Screenshot-2023-12-09-135422.png'],
					orientation: 'desc-gif'
				},
				{
					title: 'Enemy',
					description:
						'The enemy AI in this project is built using a state machine, specifically enums, to manage three main states: ROAM, PURSUIT, and HOLD. The ROAM state is the default, where the enemy moves randomly within a certain radius around the player. It calculates a roam distance and chooses random points to navigate, always staying within a defined sightline distance.',
					gifPaths: ['https://i.postimg.cc/xTdHsvj5/enemy.gif'],
					orientation: 'gif-desc'
				},

				{
					title: 'Region Analyser',
					description:
						'The Region Analyser for the WFC algorithm addresses the problem of disconnected islands in the generated map. When the map size exceeds a 20x20 grid, multiple isolated regions often form, which can prevent proper gameplay—such as when the player and enemy spawn on different islands with no path between them. The solution was to implement a method to identify and remove all but the largest island. The "CheckForDisconnectedRegionsAndConnect" method was initially designed to connect separate islands, but it was later simplified to just identify islands and remove the smaller ones, leaving only the largest connected region. The "IsNotInvalidTile" method ensures that empty tiles (" ") are ignored when identifying islands, preventing them from being treated as separate regions.',
					gifPaths: ['https://i.postimg.cc/Kj9ZfyqM/Screenshot-2024-01-21-221853.png'],
					orientation: 'desc-gif'
				},
				{
					title: 'Tile Analyser',
					description:
						'After islands are resolved, prefabs are instantiated on the grid. Each prefab includes a script to store its coordinates, which is essential for handling edge cases. Tiles at the edges of the map need special handling to ensure proper wall placement. The "TileEdgeActivation" function determines if an edge wall should remain active based on whether the neighboring tile is out of bounds or empty.',
					gifPaths: ['https://i.postimg.cc/1zNfz4WY/Screenshot-2024-01-08-204000.png'],
					orientation: 'desc-gif'
				},
				{
					title: 'Feature 3',
					description: 'Description 3',
					gifPaths: [
						'https://i.postimg.cc/q72CtQQJ/design.gif',
						'https://i.postimg.cc/vZJVHCr2/vibe.gif'
					],
					orientation: 'gif-desc'
				}
			],
			thumbnail: 'https://i.postimg.cc/13nFSyqN/thumb.png',
			engine: 'Unity',
			note: '',
			noteColor: '#ff0266',
			isSpecial: 'no'
		},
		{
			title: '2022 - Grid-based strategy',
			overview:
				'This is a Player and Card Generator for a Potential Team Management Tycoon Game, also has manual UI integration in GML.',
			videoPath: '',
			keyFeatures: [
				{
					title: 'Map',
					description:
						'The main play area of the game. The map is a 32 by 32 cell grid. Each of these grid cells represent the previously mentioned 8x8 playing grid. To do that, firstly one needs to generate Perlin noise with the correct zoom/scaling. Secondly, I used a square bump equation given by this user on reddit - (https://old.reddit.com/r/proceduralgeneration/comments/kaen7h/new_video_ on_procedural_island_noise_generation/gfjmgen/) to normalise the generated numbers (between 1 and 0) to the square bump. Literally raising and lowering land depending on their distance from the centre. Which is the third and most important step, to blend one equation with the other I must calculate the distance of each cell from the centre of the grid. Putting the two together gives a much smoother map, surrounded by water.',
					gifPaths: ['https://i.postimg.cc/CK7QVCD1/map.gif'],
					orientation: 'gif-desc'
				},
				{
					title: 'Feature 2',
					description: 'Description 2',
					gifPaths: [
						'https://i.postimg.cc/qBN4jgVn/rotation.gif',
						'https://i.postimg.cc/TwHNKRtv/cost.gif'
					],
					orientation: 'desc-gif'
				},
				{
					title: 'Playing Grid',
					description:
						'What I decided on is using layers of generated Perlin noise of different scope to spice the world with flowers, trees, rocks and colour. I then compress all these layers together into one list. The layered approach allows for different biomes such as Snow and land. The land blocks contain trees, rocks and flowers. This flora gives the land its cost. (It is calculated and shown on the main UI). Each block of land is represented by one cell. Each cell can be modified by the player. The player can sell the land for monetary gains. The player can build on the land to expand their build area.',
					gifPaths: [],
					orientation: 'gif-desc'
				},
				{
					title: 'Feature 5',
					description: '',
					gifPaths: [
						'https://i.postimg.cc/zD45M58Q/selectiondeletion.gif',
						'https://i.postimg.cc/9MRXSCSq/Screenshot-2024-01-20-111717.png'
					],
					orientation: 'gif-desc'
				},
				{
					title: 'Structures',
					description:
						'All land blocks controlled by the player can have a single structure on them, and all structures can be destroyed. To build the structures, the player must have enough resources required for its construction. All structures can be accessed straight away from the Building UI at the bottom left corner of the game. All hovered and selected land is scaled up in vertical size. This means that all object placed upon that land must follow its top, and thus know what size the Land is, and where the centre of it is. The reason the centre must be updated is because centre of the Land Block changes upon increasing the Y scale due to the fact that it is a one sided process. The land Object must not scale its Y scale in both directions.',
					gifPaths: ['https://i.postimg.cc/j5jkqWQh/building.gif'],
					orientation: 'gif-desc'
				},
				{
					title: 'Deployment',
					description:
						'Last minute feature added was unit deployment. Each playing grid loaded a newly generated navmesh that was provided in Unity. Due to time constraints, I decided not to implement my own system and not do the A* algorithm by my self. Although this is very much a supposedly temporary solution, and under perfect circumstances one would implement unit movement with the grid. Even if I had time to do the algorithm myself, I would use the Dijkstras algorithm unless I figure out the correct heuristic to turn it into an A* algorithm.',
					gifPaths: ['https://i.postimg.cc/xdG3mVgM/Screenshot-2023-04-04-010837.png'],
					orientation: 'desc-gif'
				},
				{
					title: 'Feature 5',
					description: '',
					gifPaths: [
						'https://i.postimg.cc/Y05XxdcX/movement.gif',
						'https://i.postimg.cc/Jn1ccYdg/Screenshot-2024-10-12-173607.png'
					],
					orientation: 'gif-desc'
				}
			],
			thumbnail: 'https://i.postimg.cc/tCPyGfg4/thumb.png',
			engine: 'Unity',
			note: '',
			noteColor: '#ff0266',
			isSpecial: 'no'
		},
		{
			title: '2022/24 - Trading Card Game',
			overview:
				'This trading card game was designed by me as a fun project to learn more about game design, specifically table top. The point of the game is that the players do not require anything but the cards at hand to play, and each game would consist of a Draft round similar to clash royale. This eliminates of the main card problem I find in games such as MTG and Pokemon where the cards are not made to be globally played.',
			videoPath: '',
			keyFeatures: [],
			thumbnail: 'https://i.postimg.cc/q7cfTgdP/Lester-4x.png',
			note: '',
			noteColor: '#ff0266',
			isSpecial: 'yes'
		},
		{
			title: '2023 - Genetic WFC',
			overview:
				'I Developed an automated system that uses genetic algorithms to optimize adjacency and frequency rules for large-scale pattern and layout generation.',
			videoPath: '',
			keyFeatures: [
				{
					title: 'Grids',
					description:
						'Proof of model accuracy can be seen with the command to test it. This will generate a number of grids with a spectrum of errors or in other words closeness to the correct grid from 20% to 100%. The model must then guess how correct the grid is.',
					gifPaths: [
						'https://ik.imagekit.io/jcporwfat/genetic_wfc/natcompminpoject-test-ezgif.com-video-to-gif-converter.gif?updatedAt=1726709381501'
					],
					orientation: 'gif-desc'
				},
				{
					title: 'Fitness',
					description:
						'There are different fitness functions to score the grids. One of them being tile proportion fitness and the other being the neural network fitness. The main focus being the idea that the genetic algorithm genes are rated by a neural model.',
					gifPaths: [
						'https://ik.imagekit.io/jcporwfat/genetic_wfc/natcompminpoject-MdoelTest-ezgif.com-video-to-gif-converter.gif?updatedAt=1726709378648'
					],
					orientation: 'desc-gif'
				},
				{
					title: 'Models',
					description:
						'I trained a multitude of different convolutional neural networks in tensor flow python and to test how good they were I had batch test command that would rate what the model thought and what the actual closeness was. One of the models trained did very well at recognising the correct set of rules.',
					gifPaths: [
						'https://ik.imagekit.io/jcporwfat/genetic_wfc/natcompminpoject-prediction-ezgif.com-video-to-gif-converter.gif?updatedAt=1726709384538'
					],
					orientation: 'gif-desc'
				}
			],
			thumbnail: 'https://i.postimg.cc/J4hR53WG/thumb.png',
			engine: 'Python',
			note: '',
			noteColor: '#ff0266',
			isSpecial: 'no'
		},
		{
			title: '2017-2020 - GMS Projects',
			overview:
				'This is a set of projects I had developed using Game Maker Studio, with programing done in the native GML. These are not all, but some of the projects I have worked on.',
			videoPath: '',
			keyFeatures: [
				{
					title: 'Fluid, Smooth, Fast Platformer',
					description:
						'First attempt at a non texturised platofrmer feature test. With a focus on simplicity.',
					gifPaths: [],
					orientation: 'gif-desc'
				},
				{
					title: 'Feature 2',
					description: 'Description 2',
					gifPaths: [
						'https://i.postimg.cc/jj8Cn9Pr/Lvlselect.gif',
						'https://i.postimg.cc/zBVvCjFH/login.gif'
					],
					orientation: 'desc-gif'
				},
				{
					title: 'Feature 3',
					description: 'Description 3',
					gifPaths: [
						'https://i.postimg.cc/VkWJm5Nv/jumping-collision-animation.gif',
						'https://i.postimg.cc/Y2TGxJVr/death.gif'
					],
					orientation: 'gif-desc'
				},
				{
					title: 'The idea...',
					description:
						'The point was that this platofrmer would focus on the player speedruning the levels. There s a fully working scoring system. The platofromer itself is fluid and challenging.',
					gifPaths: [],
					orientation: 'desc-gif'
				},
				{
					title: 'Feature 5',
					description: 'Description 5',
					gifPaths: [
						'https://i.postimg.cc/PNGj8bSH/additionaljump.gif',
						'https://i.postimg.cc/PfvNNSqB/trampoline.gif'
					],
					orientation: 'gif-desc'
				},
				{
					title: 'Feature 6',
					description: 'Description 6',
					gifPaths: [
						'https://i.postimg.cc/HxRxBy6Z/platform.gif',
						'https://i.postimg.cc/8k7fM1ZX/checkpoint.gif'
					],
					orientation: 'desc-gif'
				},
				{
					title: 'Gravity Change',
					description:
						'I am particularly proud of the gravity change feature, where the game flips onto the direction I choose. I had also implemented this feature such that it was very easy for me to add new levels with different gravity directions.',
					gifPaths: [],
					orientation: 'gif-desc'
				},
				{
					title: 'Feature 8',
					description: 'Description 8',
					gifPaths: [
						'https://i.postimg.cc/zfDVB5Lj/gravity.gif',
						'https://i.postimg.cc/0yszT7Ph/allatonce.gif'
					],
					orientation: 'desc-gif'
				},
				{
					title: 'Counter Strike Tycoon',
					description:
						'This is a Player and Card Generator for a Potential Team Management Tycoon Game, also has manual UI integration in GML.',
					gifPaths: [],
					orientation: 'gif-desc'
				},
				{
					title: 'Feature 2',
					description: 'Description 2',
					gifPaths: [
						'https://i.postimg.cc/DZd7BBZb/gen.gif',
						'https://i.postimg.cc/0Qq8YL8s/help.gif'
					],
					orientation: 'desc-gif'
				},
				{
					title: 'Feature 4',
					description: 'Description 4',
					gifPaths: [
						'https://i.postimg.cc/vT0bdT5Y/inspect.gif',
						'https://i.postimg.cc/zvz8MKb2/options.gif'
					],
					orientation: 'desc-gif'
				},
				{
					title: 'Clicker',
					description: 'Simple propototype for clicker type game with a self implemented carousel.',
					gifPaths: [],
					orientation: 'gif-desc'
				},
				{
					title: 'Feature 2',
					description: 'Description 2',
					gifPaths: [
						'https://i.postimg.cc/MKZpr21Z/carousel.gif',
						'https://i.postimg.cc/KcDYNvks/click.gif'
					],
					orientation: 'desc-gif'
				}
			],
			thumbnail: 'https://i.postimg.cc/ZqNbyTzH/thumb.png',
			engine: 'GMS',
			note: '',
			noteColor: '#ff0266',
			isSpecial: 'no'
		}
	];
</script>

<div style="max-width: 80%; margin: auto;">
	<div class="container">
		<header class="header">
			<Typetext />
			<h2 class="subtitle">Portfolio</h2>
		</header>
		<Separator class="my-4" />
		<Carousel.Root
			opts={{
				align: 'start',
				loop: true
			}}
			class="w-full max-w-[90%]"
		>
			<Carousel.Content class="-ml-2 md:-ml-4">
				{#each projects as project}
					<!-- Exclude the first project using slice(1) -->
					<Carousel.Item class="md:basis-1/2 lg:basis-1/3">
						<ProjectCard {...project} />
					</Carousel.Item>
				{/each}
			</Carousel.Content>
			<Carousel.Previous />
			<Carousel.Next />
		</Carousel.Root>
		<Separator class="my-4" style="margin-top: 100px" />
	</div>

	<div class="my-details">
		<h3>Contact Me</h3>
		<p>Email: a.f.1352@mail.ru</p>
		<p>
			<a href="https://www.linkedin.com/in/fedor-agafonov-93579b230/" target="_blank">LinkedIn</a>
		</p>
		<p><a href="https://github.com/coopawoopa" target="_blank">GitHub</a></p>
	</div>
</div>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');
	.features-and-gifs {
		display: flex;
		gap: 10px;
		margin: 20px;
	}
	.key-feature,
	.gif {
		flex: 1;
		max-width: 1000px;
	}

	.key-feature {
		border: 2px solid #f9f9f934;
		border-radius: 15px;
	}
	.container {
		display: flex;
		justify-content: center;
		min-height: 50vh;
		flex-direction: column;
		align-items: center;
		background-color: #f9f9f900;
		padding: 20px;
		padding-top: 100px;
	}

	.my-details {
		display: flex;
		justify-content: center;
		flex-direction: column;
		background-color: #f9f9f900;
		padding: 20px;
		min-width: 300px;
		align-items: center;
		width: 100%;
		max-width: 500px;
		margin: auto;
	}

	.header {
		text-align: center;
		margin-bottom: 20px;
		position: relative;
		z-index: 1;
		transition:
			transform 0.2s ease-in-out,
			color 0.5s ease-in-out;
	}
	.header:hover {
		transform: translate3d(0, -10px, 22px);
		color: #ff0266;
	}

	.title,
	.subtitle {
		font-family: 'Roboto', sans-serif;
		margin: 0;
		background: linear-gradient(200deg, #ff7e5f, #ffffff);
		-webkit-background-clip: text;
		-webkit-text-fill-color: transparent;
		transition: background 0.1s;
	}

	.title {
		font-weight: 700;
		font-size: 3rem;
	}

	.subtitle {
		font-weight: 400;
		font-size: 1.5rem;
	}

	.carousel-root {
		width: 100%;
		max-width: 90%;
	}

	.carousel-content {
		margin-left: -2rem;
	}

	.carousel-item {
		basis: 50%;
	}

	@media (min-width: 768px) {
		.carousel-item {
			basis: 33.3333%;
			margin-left: -4rem;
		}
	}

	@media (min-width: 1024px) {
		.title {
			font-size: 4rem;
		}

		.subtitle {
			font-size: 2rem;
		}
	}
</style>
