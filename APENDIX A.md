1.1. Defining the coordinates of the points for the first curve c_1:

xP1 = -1
yP1 = -57
zP1 = 38
xP2 = 80
yP2 = -55
zP2 = 26
xP3 = 220
yP3 = -40
zP3 = 48
xP4 = 300
yP4 = -37
zP4 = 1

1.2. Defining the points as described in Eq. 1:

P1 = (xP1, yP1, zP1)
P2 = (xP2, yP2, zP2)
P3 = (xP3, yP3, zP3)
P4 = (xP4, yP4, zP4)

1.3. Defining matrix P as described in Eq. 2:

P={{xP1,yP1,zP1},{xP2,yP2,zP2},{xP3,yP3,zP3},{xP4,yP4,zP4}}

1.4. Defining the variable u_g for each point. For the first and last points the values are known, u_1=0 and u_4=1, respectively. For u_2 and u_3 it is necessary to apply Eq. 3:

uP1 = 0
uP2 = sum(sqrt((Element(P, i+1, 1) - Element(P, i, 1))^2 + (Element(P, i+1, 2) - Element(P, i, 2))^2 + (Element(P, i+1, 3) - Element(P, i, 3))^2), i, 1, 1)/sum(sqrt((Element(P, i+1, 1) - Element(P, i, 1))^2 + (Element(P, i+1, 2) - Element(P, i, 2))^2 + (Element(P, i+1, 3) - Element(P, i, 3))^2), i, 1, Element(Dimension(P), 1)-1)
uP3 = sum(sqrt((Element(P, i+1, 1) - Element(P, i, 1))^2 + (Element(P, i+1, 2) - Element(P, i, 2))^2 + (Element(P, i+1, 3) - Element(P, i, 3))^2), i, 1, 2)/sum(sqrt((Element(P, i+1, 1) - Element(P, i, 1))^2 + (Element(P, i+1, 2) - Element(P, i, 2))^2 + (Element(P, i+1, 3) - Element(P, i, 3))^2), i, 1, Element(Dimension(P), 1)-1)
uP4 = 1

1.5. Defining the matrix T as described in Eq. 5:

Tp={{uP1^3,uP1^2,uP1,1},{uP2^3,uP2^2,uP2,1},{uP3^3,uP3^2,uP3,1},{uP4^3,uP4^2,uP4,1}}

1.6. Defining matrix A as described in Eq. 6:

Ap = Invert(Tp)*P

1.7. Storing each element a_ij of matrix A:

Ap11 = Element(Ap,1,1)
Ap12 = Element(Ap,1,2)
Ap13 = Element(Ap,1,3)
Ap21 = Element(Ap,2,1)
Ap22 = Element(Ap,2,2)
Ap23 = Element(Ap,2,3)
Ap31 = Element(Ap,3,1)
Ap32 = Element(Ap,3,2)
Ap33 = Element(Ap,3,3)
Ap41 = Element(Ap,4,1)
Ap42 = Element(Ap,4,2)
Ap43 = Element(Ap,4,3)

This step is needed because GeoGebra cannot compute further partial derivatives if these elements are not declared as unique variables. The partial derivatives are determined in section 2.1.

1.8. Defining each parametric component c_1x (u), c_1y (u) and c_1z (u) of the curve (c_1 ) ⃗, as described in the matrix multiplication in Eq. 8:

c1x(u) = Ap11*u^3+Ap21*u^2+Ap31*u+Ap41
c1y(u) = Ap12*u^3+Ap22*u^2+Ap32*u+Ap42
c1z(u) = Ap13*u^3+Ap23*u^2+Ap33*u+Ap43

1.9. Defining the spatial curve (c_1 ) ⃗(u):

c1 = Curve(c1x(u),c1y(u),c1z(u),u,0,1)

Steps 1.1 to 1.9 need to be repeated declaring new variables in order to create the two new curves (c_2 ) ⃗(u) and  (c_3 ) ⃗(u) required for the model of this paper. This can be carried out using the next subgroup of points, related to the desired curve, as shown in Table 1.

1.10. Defining each parametric component S_x (u,v), S_y (u,v) and S_z (u,v) of the surface S ⃗ as described in the matrix multiplication in Eq. 16:

Sx(u,v) = (2*v^2-3*v+1)*c1x(u)+(-4*v^2+4*v)*c2x(u)+(2*v^2-v)*c3x(u)
Sy(u,v) = (2*v^2-3*v+1)*c1y(u)+(-4*v^2+4*v)*c2y(u)+(2*v^2-v)*c3y(u)
Sz(u,v) = (2*v^2-3*v+1)*c1z(u)+(-4*v^2+4*v)*c2z(u)+(2*v^2-v)*c3z(u)

1.11. Defining the surface S ⃗:

S = Surface(Sx(u,v),Sy(u,v),Sz(u,v),u,0,1,v,0,1)
