# lowpass_filter.cpp
// C program for the above approach
#include <iostream>
#include <cmath>
#include <stdio.h>

using namespace std;

void calc_conv(int*, int*);

// Choose any length. They must
// all be equal though.
double x[10], h[10], y[10];

int l1, l2 = 0;
double w = 1;
double pi = acos(-1);

// Driver code
int main()
{
    printf("Enter the length of the first sequence: ");
    scanf("%d", &l1);
    printf("Enter the length of the second sequence: ");
    scanf("%d", &l2);
    printf("Enter cutoff frequency of the filter: ");
    scanf("%lf", &w);

    // Delegating calculation to a
    // separate function.
    calc_conv(&l1, &l2);
    return 0;
}
// Normalized sinc(x) = sin(pi * x) / (pi * x)
double sinc_normalized(double x) {
    if (x == 0.0) {
        return 1.0;
    }
    double pi_x = pi * x;
    return sin(pi_x) / pi_x;
}

void calc_conv(int* len1, int* len2)
{
    int l = (*len1) + (*len2) - 1;
    int i, j, n, k = 0;

    // Getting values of 1st sequence
    for (i = 0; i < *len1; i++) {
        printf("Enter x[%d]:",i);
        scanf("%lf", &x[i]);
    }
    
    // Defining filter
    for (j = 0; j < *len2; j++) {
        h[j] = (w/pi)*sinc_normalized(j*w/pi);
    }

    for (n = 0; n < l; n++) {
        y[n] = 0;
        for (k = 0; k < *len1; k++) {

            // To right shift the impulse
            if ((n - k) >= 0
                && (n - k) < *len2) {

                // Main calculation
                y[n] = y[n] + x[k] * h[n - k];
            }
            
        }
      printf("%lf\t", y[n] );
    }
}
