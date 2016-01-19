package com.app.nightvip;

import android.app.Activity;
import android.content.Intent;
import android.content.pm.PackageInfo;
import android.content.pm.PackageManager.NameNotFoundException;
import android.os.Bundle;
import android.view.Menu;
import android.view.MenuInflater;
import android.view.MenuItem;
import android.view.View;
import android.view.View.OnClickListener;
import android.view.Window;
import android.widget.ImageButton;
import android.widget.TextView;
import android.widget.Toast;

public class Inicio extends Activity implements OnClickListener {
	
	private ImageButton restaurante, pub, disco;
	TextView textoBajoLogoPpal;
	String actualizar, accesoDiscos, accesoPubs, accesoRest;
	int versionMarket, versionMovil;
    Toast t;
    Utilidades utilidades = new Utilidades(this);
    Gps gps;
    double latitud, longitud;
	
    @Override
    public void onCreate(Bundle savedInstanceState) {
    	//hacemos que la pantalla sea sin titulo 
		//hay q hacerlo antes del setcontentview o setlistadapter, ...
    	requestWindowFeature(Window.FEATURE_NO_TITLE);
    	super.onCreate(savedInstanceState);
    	//si se inicia la actividad con el boolean SALIR, se sale de la app antes de hacer nada
    	if(getIntent().getBooleanExtra("SALIR", false)){//si el valor fuera true aqui, nunca empezaria la app
    		finish();
    	}else{
		
	        setContentView(R.layout.inicio);
	        declaraVar();
	        
	        Bundle preDatos = getIntent().getExtras();
	        versionMarket = Integer.parseInt(preDatos.getString("version"));
	        actualizar = preDatos.getString("actualizar");
	        accesoDiscos = preDatos.getString("discotecas");
	        accesoPubs = preDatos.getString("pubs");
	        accesoRest = preDatos.getString("restaurantes");
	        
	        //nightVipWeb.setOnClickListener(this);
	        disco.setOnClickListener(this);
	        restaurante.setOnClickListener(this);
	        pub.setOnClickListener(this);
	        PackageInfo pInfo;//para coger la version instalada
			try {
				pInfo = getPackageManager().getPackageInfo(getPackageName(), 0);
		        versionMovil = pInfo.versionCode;
		        if(versionMarket > versionMovil){
		        	if(actualizar.equalsIgnoreCase("si")){
		        		utilidades.mostrarAlertDialog(this, "Se recomienda actualizar", "Hay una actualizaci�n de la App " +
		        				"en Google Play con mejoras significativas.", null, "alMarket");
		        		
		        	}else{
		        		t = Toast.makeText(getApplicationContext(), "Hay una actualizaci�n de la App en Google Play."
		        				, Toast.LENGTH_SHORT);
		        		t.show();
		        		////////////////////////////
		        		/*Uri url = Uri.parse("http://nightvip.es");
	                	Intent i = new Intent(Intent.ACTION_WEB_SEARCH, url);
	                	startActivity(i);*/
	                	/////////////////////////////
		        	}
		        }
			} catch (NameNotFoundException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
			gps = new Gps(this);
			if(gps.tengoPosicion){
				latitud = gps.cogeLatitud();
				longitud = gps.cogeLongitud();
			}
    	}
        
    }

	private void declaraVar() {
		// TODO Auto-generated method stub
		//nightVipWeb =(ImageButton)findViewById(R.id.ibNightVipWeb);
		//nightVipWeb.setBackgroundColor(color.black);
		restaurante =(ImageButton)findViewById(R.id.ibRestaurantes);
		pub = (ImageButton)findViewById(R.id.ibPubs);
		disco = (ImageButton)findViewById(R.id.ibDisco);
		//textoBajoLogoPpal = (TextView)findViewById(R.id.tvBajoLogoPpal);
		//textoBajoLogoPpal.setText(Html.fromHtml("<i>tus noches gratis</i>"));
	}

	public void onClick(View arg0) {
		// TODO Auto-generated method stub
		
		
		Intent i;
		//paso la posicion para calcular las distancias
		Bundle posicion = new Bundle();
		posicion.putDouble("latitud", latitud);
		posicion.putDouble("longitud", longitud);
		
		switch(arg0.getId()){
		case R.id.ibDisco:
			if (utilidades.estaConectado()) {//compruebo si est� conectado a internet
				if (accesoDiscos.equalsIgnoreCase("si")) {
					i = new Intent(Inicio.this, Discotecas.class);
					i.putExtras(posicion);
					startActivity(i);
				} else {
					utilidades.mostrarAlertDialog(this, "Lo sentimos",
							"Opci�n temporalmente inhabilitada.", false, null);
				}
			}else// si no est� conectado avisa, pero no cierra
				utilidades.mostrarAlertDialog(this, "Error", "No est�s conectado a internet", false, null);
			break;
			
		case R.id.ibPubs:
			if (utilidades.estaConectado()) {//compruebo si est� conectado a internet
				if (accesoPubs.equalsIgnoreCase("si")) {
					i = new Intent(Inicio.this, Pubs.class);
					i.putExtras(posicion);
					startActivity(i);
				} else {
					utilidades.mostrarAlertDialog(this, "Lo sentimos",
							"Opci�n temporalmente inhabilitada.", false, null);
				}
			}else// si no est� conectado avisa, pero no cierra
				utilidades.mostrarAlertDialog(this, "Error", "No est�s conectado a internet", false, null);
			break;
			
		case R.id.ibRestaurantes:
			if (utilidades.estaConectado()) {//compruebo si est� conectado a internet
				if (accesoRest.equalsIgnoreCase("si")) {
					i = new Intent(Inicio.this, Restaurantes.class);
					i.putExtras(posicion);
					startActivity(i);
				} else {
					utilidades.mostrarAlertDialog(this, "Lo sentimos",
							"Opci�n temporalmente inhabilitada.", false, null);
				}
			}else// si no est� conectado avisa, pero no cierra
				utilidades.mostrarAlertDialog(this, "Error", "No est�s conectado a internet", false, null);
			break;
		
		
	
		
		}
		
	}

	
	//EL MENU DESPLEGABLE QUE SALE AL DARLE A LA TECLA DE OPCIONES
	@Override
	public boolean onCreateOptionsMenu(Menu menu) {
		// TODO Auto-generated method stub
		//si se inicia la actividad con el boolean SALIR, se sale de la app antes de hacer nada
    	if(getIntent().getBooleanExtra("SALIR", false)){//si el valor fuera true aqui, nunca empezaria la app
    		finish();
    	}
		super.onCreateOptionsMenu(menu);
		MenuInflater opciones = getMenuInflater();
		opciones.inflate(R.menu.menu, menu);
		return true;
	}

	@Override
	public boolean onOptionsItemSelected(MenuItem item) {
		// TODO Auto-generated method stub
		super.onOptionsItemSelected(item);
		Intent i;
		switch(item.getItemId()){
		case R.id.MENUquienesSomos:
			//"tematizacion" en el manifiesto
			i = new Intent("com.app.nightvip.SOBRENOSOTROS");
			startActivity(i);
			
			break;
		case R.id.MENUSalir:
			finish();
			break;
		}
		return false;//en ppio da igual false q true
	}
	
}
