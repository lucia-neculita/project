# project
#include <stdio.h>
struct tableta {
	char producator[20];
	char model[20];
	int an;
	float pret;

};
int main() {
	struct tableta a[10];
	int n = 0;//nr tablete
	float s = 0;//suma totala a tabletelor
	FILE *f1, *f2;
	f1 = fopen("citire.txt", "r");
	f2 = fopen("afisare.txt", "w");

	if (!f1) {
		printf("Fisierul citire nu exista!");
		fflush(stdout);
		return 1;
	}

	while (fscanf(f1, "%s%s%d%f", a[n].producator, a[n].model, &a[n].an,
			&a[n].pret) != EOF) {
		printf("Tableta %s  de model  %s fabricata in %d, are pretul %.2f lei\n",
				a[n].producator, a[n].model, a[n].an, a[n].pret);
		fflush(stdout);
		n++;
	}
	printf("\n");
	fflush(stdout);

	struct tableta aux;
	fprintf(f2, "ordonarea crescatoare a preturilor este:\n");
	for (int i = 0; i < n; i++) {
		for (int j = i + 1; j < n; j++) {
			if (a[i].pret > a[j].pret) {
				aux = a[i];
				a[i] = a[j];
				a[j] = aux;
			}
		}
		fprintf(f2, "%s %s %.2f lei\n",a[i].producator, a[i].model, a[i].pret);
		fflush(stdout);

	}

	float media;
	for (int i = 0; i < n; i++) {
		s = s + a[i].pret;
	}
	media = (float) s / n;
	fprintf(f2, "Media preturilor este:%.2f lei", media);
	fflush(stdout);

	return 0;
}
