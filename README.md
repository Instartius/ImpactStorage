ImpactStorage - Local Storage plugin for ImpactJS
=================================================

h2. About
ImpactStorage is a plugin for HTML5/js game framework "ImpactJS":http://www.impactjs.com/ to give developers quick access to localStorage for their projects. Mostly an interface for localStorage, ImpactStorage is set up to bake with your ImpactJS project, take care of some error handling, as well as support object types in addition to strings.

Created by "Jordan Santell":http://www.jsantell.com/ for "Duck It!":http://www.spacewhalestudios.com/duckit/; enjoy!

h2. Installation
* Move impact-storage.js to your ImpactJS project's plugin folder: ``[PROJECT]/lib/plugins/impact-storage.js``
* Add the plugin to your main.js file
<pre>
    ig.module(
        'game.main'
    )
    .requires(
        'impact-game',
        ...
        'plugins.impact-storage',
        ...
    )
</pre>
*Create a local storage object and check out the examples and methods below
    
    storage: new ImpactStorage(),



h2. Methods
``isCapable()``: Returns ``true`` if the browser is capable of using localStorage. ``false`` otherwise.
``isSet(key)``: Returns ``true`` if ``key`` has been set in localStorage. ``false`` otherwise.
``initUnset(key, value)``: *Iff* ``key`` has not been set, set ``key`` to ``value``
``get(key)``: Returns the value associated with ``key`` in localStorage as a ``string``, or an ``object`` if parsable by JSON.
``getInt(key)``: Returns the value associated with ``key`` in localStorage as an ``int``.
``getFloat(key)``: Returns the value associated with ``key`` in localStorage as a ``float``.
``getBool(key)``: Returns the value associated with ``key`` in localStorage as a ``bool``. Returns ``null`` if ``value`` is not ``0``, ``1``, ``false`` or ``true``.
``key(n)``: Returns the value of the key stored at position ``n`` in localStorage.
``set(key, value)``: Sets an item in localStorage with the ``key`` ``value`` pair. Overwrites the previous value of ``key`` if it existed previously. ``value`` is stored as either a ``string`` or an ``object``.
``setHighest(key, value)``: Sets an item in localStorage with the ``key`` ``value`` pair *iff* the currently stored ``value`` is smaller.
``remove(key)``: Removes the item with the specified ``key``.
``clear()``: Clears all localStorage data associated with this origin.


h2. Examples
h3. High Score
<pre>
    this.storage = new ImpactStorage();

    // Initialize high score as 0 if no high score exists
    this.storage.initUnset('highScore', 0);
</pre>
During the update loop that determines whether or not the current score should override the score in localStorage:
<pre>
    var player = this.getEntitiesByType(EntityPlayer)[0];
    // Updates the value of 'highScore' if and only
    // if player.score > this.storage.get('highScore')
    this.storage.setHighest('highScore',player.score); 
</pre>

h3. Storing JSON Objects
localStorage stores all data as strings, but the ImpactStorage ``.set(key, value)`` and ``.get(key)`` methods convert objects to and from strings  in order to be saved to localStorage.
<pre>

    this.storage = new ImpactStorage();

    // Player's velocity is an object stored as
    // vel: {x: 200, y: 100}
    // And that data is now being stored with key playerVel in localStorage
    var player = this.getEntitiesByType(EntityPlayer)[0];
    this.storage.set('playerVel',player.vel)

    // And let's output it for fun
    alert("Player's x velocity: "+this.storage.get('playerVel').x);
    alert("Player's y velocity: "+this.storage.get('playerVel').y);

</pre>

h2. More Information
