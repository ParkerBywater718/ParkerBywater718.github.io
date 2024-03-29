**Routine Name:** LU  

**Author:** Parker Bywater

**Language:** Java. This can be compiled using an appropriate Java compiler. 

**Description/Purpose:** This routine computes the LU-factorization of a square matrix.  

**Input:** A square matrix represented as a 2-dimensional array of doubles. 
 
**Output:** This routine returns the LU-factorization of the matrix as two seperate entities.  

**Implementation/Code:** The following is the code for LU. 
```java 
public static double[][][] LU(double[][] A) {
    if (A.length == 0)
        throw new IllegalArgumentException("Matrix cannot be empty");

    double[][] L = new double[A.length][A.length];
    for (int i = 0; i < L.length; i++)
        L[i][i] = 1;
    
    double[][] U = new double[A.length][A.length];
    for (int i = 0; i < A.length; i++)
        System.arraycopy(A[i], 0, U[i], 0, A.length);
    
    for (int k = 0, r = 0; k < U.length; k++, r++) {
        if (U[r][k] != 0) {
            double pivot = U[r][k];
            for (int i = r + 1; i < U.length; i++) {
                double multiplier = U[i][k] / pivot;
                // U[r] = U[r] - multiplier * U[r-1]
                for (int j = 0; j < U[r].length; j++) {
                    U[i][j] = U[i][j] - multiplier * U[r][j];
                }
                L[i][k] = multiplier;
            }

        }
    }

    return new double[][][]{L, U};
}  
```

**Usage/Example:** Sample output for the matrix A = 

    19.8241	    1.9444	   14.4131	    3.9102	    5.0844	
    12.6527	    8.7957	   19.6549	   18.4340	   11.4366	
    0.7599	    9.9567	    5.6679	    8.1733	   12.3671	
    7.1706	    8.9150	   20.2907	   19.6673	   15.9366	
    14.8775	   14.3102	    2.3970	   18.8819	   14.3528 

The output is then L = 
    
    1.0000	    0.0000	    0.0000	    0.0000	    0.0000	
    0.6383	    1.0000	    0.0000	    0.0000	    0.0000	
    0.0383	    1.3081	    1.0000	    0.0000	    0.0000	
    0.3617	    1.0870	   -0.4336	    1.0000	    0.0000	
    0.7505	    1.7011	    3.0608	   -6.0638	    1.0000	

and U = 

    19.8241	    1.9444	   14.4131	    3.9102	    5.0844	
     0.0000	    7.5546	   10.4557	   15.9384	    8.1915	
    -0.0000	    0.0000	   -8.5617	  -12.8255	    1.4570	
    -0.0000	    0.0000	    0.0000	   -4.6326	    5.8253	
    -0.0000	    0.0000	    0.0000	    0.0000	   27.4671

**Last Modified:** 11/8/19 
