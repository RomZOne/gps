#include <stdio.h>
#include <string.h>
#include <memory.h>
#include <stdlib.h>
#define MAXSIZE 256

typedef struct {
int heure;
int minut;
int secon;
} temps;

typedef struct {
int degre;
int minut;
double secon;
} latitude;

typedef struct {
int degre;
int minut;
double secon;
} longiture;

typedef struct {
    int position;
} positionnement;

typedef struct {
    int sat;
} nbsat;

void decode_GPGGA(char *stringRead);
int main(void) {

//
char stringRead[MAXSIZE];	 // buffer pour recevoir les trames, MAXSIZE = 256

FILE *gpsFile;

gpsFile = fopen("gps.TXT","r");
if(gpsFile == NULL)
{
printf("Erreur d'ouverture du fichier\n");
return -1;
}
while(fgets(stringRead,MAXSIZE,gpsFile) !=NULL)	// Lecture d'une trame complète
{
(memcmp(stringRead,"$GPGGA",6)==0);
{
decode_GPGGA(stringRead);
}
}
fclose(gpsFile);
return (0);
} //fin main

void decode_GPGGA(char *stringRead)
{
char *debut, *med,*fin, tmpbuff[32];
int l;
latitude theLatitude;
longiture theLongiture;
temps monTemps;
positionnement thePosition;
nbsat satellites;
printf("Ce programme ne sait decoder que des trames de type GPGGA\n");
memset(tmpbuff,0x00,32);	 // Initialisation de tmpbuff à 0x00h
debut = strstr(stringRead,",")+1;	// On cherche la première ","

fin = strstr(debut,",");	 // On cherche la première ","
l = fin - debut;
med = strstr(debut,".");	 // On cherche le point "."

memcpy(&tmpbuff,debut,2);	 // On l'heure (2 chiffres)
monTemps.heure = atoi(tmpbuff);	 // On converti en numérique grace a la fonction atoi

memcpy(&tmpbuff,debut+2,2);	 // Idem pour les minutes
monTemps.minut = atoi(tmpbuff);	 // Idem

memcpy(&tmpbuff,debut+4,2);	 // Idem pour les secondes pas de centièmes
monTemps.secon = atoi(tmpbuff);	 // Convertion en numérique

printf("Heure %2d:%2d:%2d\n",monTemps.heure,monTemps.minut,monTemps.secon);

// Décodage Latitude
debut = strstr(debut,",")+1;	 // On cherche la première ","
med = strstr(debut,".");	 // On cherche le point "."
fin = strstr(debut,",");	 // On cherche la suivante ","
memcpy(&tmpbuff,debut,2);	 // Récupération des degrés
theLatitude.degre = atoi(tmpbuff);	// On converti en numérique

memcpy(&tmpbuff,debut+2,2);	 // Idem pour les minutes
theLatitude.minut = atoi(tmpbuff);	// Atoi permets de convertir de l'ASCII en valeur entiere

l = (fin - med);	 // Nombre de décimales pour les secondes (en degrés)
memcpy(&tmpbuff,debut+4,l);	 // On les récupère
theLatitude.secon = (atof(tmpbuff))*60.0;	// ASCII => int => en secondes
debut = strstr(debut,",")+1;	 // On cherche la première ","
// On affiche le tout (y compris N/S)
printf("Latitude %2d-%2d-%2.3f %1.1s\n",theLatitude.degre,theLatitude.minut,theLatitude.secon,debut);

// Décodage Longitude

memset(tmpbuff,0x00,32);
debut = strstr(debut,",")+1;	 // On cherche la première ","
med = strstr(debut,".");	 // On cherche le point "."
fin = strstr(debut,",");	 // On cherche la suivante ","
memcpy(&tmpbuff,debut,3);	 // Récupération des degés
theLongiture.degre = atoi(tmpbuff);	// On converti en numérique

memset(tmpbuff,0x00,32);
memcpy(&tmpbuff,debut+3,2);	 // Idem pour les minutes
theLongiture.minut = atoi(tmpbuff);	// ASCII => Numérique

memset(tmpbuff,0x00,32);
l = (fin - med);	 // Nombre de décimales pour les secondes (en degrés)
memcpy(&tmpbuff,debut+5,l);	 // On les récupère
theLongiture.secon = (atof(tmpbuff))*60.0;	// ASCII => Numérique => en secondes
debut = strstr(debut,",")+1;	 // On cherche la première ","
printf("Longitude %3d %2d %2.3f %1.1s\n",theLongiture.degre,theLongiture.minut,theLongiture.secon,debut);


// Position

memset(tmpbuff,0x00,32);
debut = strstr(debut,",")+1;	 // On cherche la première ","
med = strstr(debut,".");	 // On cherche le point "."
fin = strstr(debut,",");	 // On cherche la suivante ","
memcpy(&tmpbuff,debut,1);	 // Récupération de la position
thePosition.position = atoi(tmpbuff);
printf("Position %d\n",thePosition.position);

// Nombre de satellites (affiche qu'un seul chiffre)
memset(tmpbuff,0x00,32);
debut = strstr(debut,",")+2;	 // On cherche la première ","
med = strstr(debut,".");	 // On cherche le point "."
fin = strstr(debut,",");	 // On cherche la suivante ","
memcpy(&tmpbuff,debut,1);	 // Récupération de la position
satellites.sat = atoi(tmpbuff);
printf("Nombre de satellites (n'affiche qu'un chiffre) %d\n", satellites.sat);
}

