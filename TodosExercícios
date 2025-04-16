#include <GL/freeglut.h>
#include <iostream>
#include <cmath>

using namespace std;

int opcao = 0;
float yQuadrado = -0.5f;
float xQuadrado = -0.9f;
bool indoPraDireita = true;
float anguloCirculo = 0.0f;

void barco() {
    glClear(GL_COLOR_BUFFER_BIT);

    glClearColor(1.0f, 0.97f, 0.85f, 1.0f);

    glColor3f(1.0f, 0.0f, 0.0f); 
    glBegin(GL_POLYGON);
    glVertex2f(-0.6f, -0.4f);
    glVertex2f(0.6f, -0.4f);
    glVertex2f(0.4f, -0.6f);
    glVertex2f(-0.4f, -0.6f);
    glEnd();

    glColor3f(0.75f, 0.75f, 0.75f);
    glBegin(GL_TRIANGLES);
    glVertex2f(-0.022f, 0.3f);
    glVertex2f(-0.3f, -0.2f);
    glVertex2f(0.5f, -0.2f);
    glEnd();

    glColor3f(0.5f, 0.25f, 0.0f);
    glBegin(GL_QUADS);
    glVertex2f(-0.03f, -0.4f);
    glVertex2f(0.03f, -0.4f);
    glVertex2f(0.03f, 0.3f);
    glVertex2f(-0.03f, 0.3f);
    glEnd();

    glColor3f(0.2f, 0.2f, 0.8f);
    glBegin(GL_QUADS);
    glVertex2f(-0.028f, 0.3f);
    glVertex2f(0.2f, 0.3f);
    glVertex2f(0.2f, 0.38f);
    glVertex2f(-0.028f, 0.38f);
    glEnd();

    glFlush();
}

void alvo() {
    glClear(GL_COLOR_BUFFER_BIT);

    float cores[3][3] = {
        {0.0f, 0.0f, 0.4f},
        {0.0f, 0.0f, 0.7f},
        {1.0f, 1.0f, 1.0f}
    };

    float raios[] = { 0.6f, 0.4f, 0.2f };

    for (int i = 0; i < 3; i++) {
        glColor3f(cores[i][0], cores[i][1], cores[i][2]);
        glBegin(GL_TRIANGLE_FAN);
        glVertex2f(0.0f, 0.0f);
        for (int j = 0; j <= 360; j++) {
            float rad = j * 3.14159f / 180.0f;
            glVertex2f(cos(rad) * raios[i], sin(rad) * raios[i]);
        }
        glEnd();
    }

    glFlush();
}

void quadradoSubindo() {
    glClear(GL_COLOR_BUFFER_BIT);

    glPushMatrix();
    glTranslatef(0, yQuadrado, 0);
    glColor3f(1, 0, 0);
    glBegin(GL_QUADS);
    glVertex2f(-0.2f, -0.2f);
    glVertex2f(0.2f, -0.2f);
    glVertex2f(0.2f, 0.2f);
    glVertex2f(-0.2f, 0.2f);
    glEnd();
    glPopMatrix();

    glFlush();
}

void quadradoAndando() {
    glClear(GL_COLOR_BUFFER_BIT);

    glPushMatrix();
    glTranslatef(xQuadrado, -0.5f, 0);
    glColor3f(0.5f, 0, 0.5f);
    glBegin(GL_QUADS);
    glVertex2f(-0.1f, -0.1f);
    glVertex2f(0.1f, -0.1f);
    glVertex2f(0.1f, 0.1f);
    glVertex2f(-0.1f, 0.1f);
    glEnd();
    glPopMatrix();

    glFlush();
}

void circuloGirando() {
    glClear(GL_COLOR_BUFFER_BIT);

    glPushMatrix();
    glRotatef(anguloCirculo, 0, 0, 1);

    glBegin(GL_TRIANGLE_FAN);

    glColor3f(1, 1, 1);
    glVertex2f(0, 0);

    int totalPontos = 100;
    float raio = 0.5f;

    for (int i = 0; i <= totalPontos; i++) {
        float ang = 2 * 3.14159f * i / totalPontos;

        float r = fabs(cos(ang));
        float g = fabs(sin(ang));
        float b = fabs(cos(ang + 1.57f));

        glColor3f(r, g, b);
        glVertex2f(cos(ang) * raio, sin(ang) * raio);
    }

    glEnd();
    glPopMatrix();

    glFlush();
}

void mostrarCena() {
    if (opcao == 1) barco();
    else if (opcao == 2) alvo();
    else if (opcao == 3) quadradoSubindo();
    else if (opcao == 4) quadradoAndando();
    else if (opcao == 5) circuloGirando();
    else {
        glClear(GL_COLOR_BUFFER_BIT);
        glFlush();
    }
}

void teclado(unsigned char tecla, int x, int y) {
    if (tecla == 32 && opcao == 3) {
        yQuadrado += 0.05f;
        glutPostRedisplay();
    }
}

void animar(int valor) {
    if (opcao == 4) {
        xQuadrado += indoPraDireita ? 0.02f : -0.02f;
        if (xQuadrado > 0.9f || xQuadrado < -0.9f)
            indoPraDireita = !indoPraDireita;
    }

    if (opcao == 5) {
        anguloCirculo += 5;
        if (anguloCirculo > 360)
            anguloCirculo = 0;
    }

    glutPostRedisplay();
    glutTimerFunc(16, animar, 0);
}

int main(int argc, char** argv) {
    cout << "Escolha o que quer ver:\n";
    cout << "1 - Barco\n";
    cout << "2 - Alvo\n";
    cout << "3 - Quadrado que sobe (espaco)\n";
    cout << "4 - Quadrado animado\n";
    cout << "5 - Circulo girando\n";
    cin >> opcao;

    glutInit(&argc, argv);
    glutInitWindowSize(600, 600);
    glutCreateWindow("Desenhos OpenGL");
    glutInitDisplayMode(GLUT_SINGLE | GLUT_RGB);
    glutDisplayFunc(mostrarCena);
    glutKeyboardFunc(teclado);
    glutTimerFunc(0, animar, 0);
    glClearColor(1, 1, 1, 1);
    glutMainLoop();

    return 0;
}
