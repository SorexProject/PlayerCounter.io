# PlayerCounter 
## Description 
il permet d'afficher le nombre de joueur dans les servers pterodactyl
## Configure 
- /routes/admin.php
<p>
Please paste this lines to /routes/admin.php to the bottom of the file
</p>

```
|--------------------------------------------------------------------------
| Player Counter Controller Routes
|--------------------------------------------------------------------------
|
| Endpoint: /admin/players
|
*/
Route::group(['prefix' => 'players'], function () {
    Route::get('/', 'PlayerCounterController@index')->name('admin.players');

    Route::post('/create', 'PlayerCounterController@create')->name('admin.players.create');
    Route::post('/update', 'PlayerCounterController@update')->name('admin.players.update');

    Route::delete('/delete', 'PlayerCounterController@delete')->name('admin.players.delete');
});
```
- /routes/api-client.php
<p>
Please paste this line to /routes/api-client.php above the ***Route::group(['prefix' => '/settings'], function () { line***
</p>
```
Route::get('/players', 'Servers\PlayersController@index');

```
- /resources/views/layouts/admin.blade.php
<p>
Please paste this lines to /resources/views/layouts/admin.blade.php above the <li class="header">SERVICE MANAGEMENT</li> line
</p>
```
<li class="{{ ! starts_with(Route::currentRouteName(), 'admin.players') ?: 'active' }}">
	<a href="{{ route('admin.players') }}">
		<i class="fa fa-user"></i> <span>Player Counter</span>
	</a>
</li>
```
- /resources/scripts/components/server/ServerConsole.tsx
<p>
Please paste this line to /resources/scripts/components/server/ServerConsole.tsx under the import PowerControls from '@/components/server/PowerControls'; line
</p>
```
import PlayerCounter from '@/components/server/PlayerCounter';
```
<p>
Please paste this line to /resources/scripts/components/server/ServerConsole.tsx above the <Can action={[ 'control.start', 'control.stop', 'control.restart' ]} matchAny> </Can> line 
</p>

```
<PlayerCounter></PlayerCounter>
```	
- /resources/scripts/components/dashboard/ServerRow.tsx
<p>
Please paste this line to /resources/scripts/components/dashboard/ServerRow.tsx under the import styled from 'styled-components/macro'; line
</p>
```
import PlayerCounter from '@/components/dashboard/PlayerCounter';
```
<p>
Please paste this line to /resources/scripts/components/dashboard/ServerRow.tsx under the <React.Fragment> line
</p>
```
<PlayerCounter uuid={server.uuid}></PlayerCounter>
```
## Finalization
<p>
After all code inserted to code and app and resources and database and vendor folder pasted. Please run this commands (node is required, min version: v13.x [node -v]):
</p>
- co mposer require austinb/gameq:~3.0
- npm i -g yarn
- cd /var/www/pterodactyl
- yarn install
- yarn run build:production
- php artisan route:clear && php artisan cache:clear && php artisan view:clear
- php artisan migrate
