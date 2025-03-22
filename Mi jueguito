#include<iostream>
using namespace std;
#include "miniwin.h"
using namespace miniwin;

#include <cstdlib> 

#include <list>
using namespace std;

const int XTAM = 50, YTAM=30;
const int SZ = 12;
struct Punto {
	int x, y;
};

void cuadrado(const Punto& p, int c){
	color(c);
	rectangulo_lleno(p.x*SZ, p.y*SZ, (p.x+1)*SZ-1, (p.y+1)*SZ-1);
}

bool hay_choque(const Punto& cabeza, const list<Punto>& cola){
	if (cabeza.x >= XTAM || cabeza.x < 0) {
	 return true;
	}
	if (cabeza.y >= XTAM || cabeza.y < 0) {
	return true;	
	}
	list<Punto>::const_iterator it;
	for (it = cola.begin(); it != cola.end(); it++){
		if (cabeza.x == it->x && cabeza.y == it->y){
			return true;
			
		}
	}
	return false;
}

Punto al_azar() {
	Punto p = { rand() %XTAM, rand() %YTAM };
	return p;	
}


void jugar(int velocidad){
	vredimensiona(XTAM * SZ, YTAM * SZ);
	Punto cabeza = { 30, 20 };
	Punto comida = al_azar();
	list<Punto> cola;
	int vx = 1, vy = 0; 
	int retraso = 0, engorda = 0;
	int t = tecla();
	bool chocar = false, continuar=true;
	
	while (t != ESCAPE && !chocar){
		retraso++;
		//logica del juego
		if (t == ARRIBA){
			vx = 0, vy = -1;
		}
		else if (t == ABAJO){
			vx = 0, vy = 1;
		}
		else if (t == IZQUIERDA){
			vx = -1, vy = 0;
		}
		else if (t == DERECHA){
			vx = 1, vy =0;
		}
		if (retraso == 10){
		   cola.push_front (cabeza);
		   if(engorda > 0){
		   	engorda--;
		   }
		   else{
		   cola.pop_back();
		   }
		   cabeza.x += vx;
		   cabeza.y += vy;
		   if(hay_choque(cabeza, cola)){
		   	chocar = true;
		   }
		   else if (cabeza.x == comida.x && cabeza.y == comida.y){
		   	engorda = 3;
		   	comida = al_azar();
		   }
		   while (hay_choque(comida, cola) ||
		          comida.x == cabeza.x && comida.y == cabeza.y){
			   comida = al_azar();
			}
		   retraso = velocidad;
		}
		if (!chocar){
		    //pintar
		    borra();
		    list<Punto>::const_iterator it;
		    for (it = cola.begin(); it != cola.end(); it++) {
		     	cuadrado(*it, ROJO);
		     	cuadrado(comida, VERDE);
		    }
		   cuadrado(cabeza, AZUL);
		   cuadrado (comida, VERDE);
		   refresca();
		}
		espera(1);
		t = tecla();
	}
}

void mostrar_dificultad(){
	texto(100, 50, "Selecciona una opcion:");
    texto(100, 100, "1: FACIL");
    texto(100, 130, "2: INTERMEDIO");
    texto(100, 160, "3: DIFICIL");
    texto(100, 190, "4: SALIR");
    
}

void mostrar_menu() {
    texto(100, 50, "Selecciona una opcion:");
    texto(100, 100, "1: JUGAR");
    texto(100, 130, "2: CONFIGURAR DIFICULTAD");
    texto(100, 160, "3: SALIR");
    texto(100, 200, "Hecho por Mario Ivan Rodriguez Guzman");
    texto (100, 230, "LEVN202");
}

int main() {
    vredimensiona(XTAM * SZ, YTAM * SZ);;
    int velocidad = 6;
    bool en_principal = true;  
    bool en_dificultad = false; 
    borra();
    while (en_principal) {
    	refresca();
        mostrar_menu();  // Mostrar el menú principal
        int tecla_principal = tecla(); 

        switch (tecla_principal) {
        	borra();
        	refresca();
            case '1':  // Opción JUGAR
                texto(100, 150, "Has seleccionado JUGAR");
                borra();
                jugar(velocidad);
                refresca();
                espera(20);
                break;

            case '2': 
                en_dificultad = true;  
                borra();
                while (en_dificultad) {
                	refresca();
                    mostrar_dificultad();  
                    int tecla_dificultad = tecla();  
                    switch (tecla_dificultad) {
                        case '1':  // Opción Facil
                            borra();
                            texto(250, 150, "Dificultad: Facil");
                            velocidad=4;
                            refresca();
                            espera(200);
                            break;

                        case '2': 
                            borra();
                            velocidad=6;
                            texto(250, 150, "Dificultad: Intermedio");
                            refresca();
                            espera(200);
                            break;

                        case '3': 
                            borra();
                            velocidad=8;
                            texto(250, 150, "Dificultad: Dificil");
                            refresca();
                            espera(200);
                            break;

                        case '4' :  
                            en_dificultad = false; 
                            borra();
							break;
                    }
                }
                break;

            case '3': 
                en_principal = false; 
                break;

        }
    }
    return 0;
}
