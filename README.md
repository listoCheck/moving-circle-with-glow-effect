
#include <cmath>
#include <iostream>
#include <stdio.h>
#include <string.h>
using namespace std;


int main(){ 
	int width = 120;
	int height = 30;
	float aspect = (float)width / height;
	float pixelAspect = 11.0f / 22.0f;
	char gradient[] = " .:!/%$@";
	int gradientSize = std::size(gradient) - 2;

	char* screen = new char[width * height + 1];
	screen[width * height] = '\0';
	for (int t = 0; t < 10000000000; t++) {
		for (int i = 0; i < width; i++) {
			for (int j = 0; j < height; j++) {
				float x = (float)i / width * 2.0f - 1.0f;
				float y = (float)j / height * 2.0f - 1.0f;
				x *= aspect * pixelAspect;
				x += sin(t * 0.001);
				char pixel = ' ';
				//if (x * x + y * y < 0.5) pixel = '#';
				//screen[i + j * width] = pixel;
				float dist = sqrt(x * x + y * y);
				int color = (int)(1.0f / dist);
				if (color < 0) color = 0;
				else if (color > gradientSize) color = gradientSize;
				pixel = gradient[color];
				screen[i + j * width] = pixel;
			}
		}
		printf("%s", screen);
	}
	
	//cout << screen;
	return 0;
}

