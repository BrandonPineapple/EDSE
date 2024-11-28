
#include <stdbool.h>
#include <stdint.h>
#include "inc/tm4c1294ncpdt.h"
#include "func.h"

/*
 * Definiciones de las variables a emplear
 */

uint16_t ADC_result;
uint16_t ADC_result1;
uint16_t ADC_result2;
uint16_t ADC_result3;
float temperature;

//Direccion de sensores
uint8_t INA_Address=0x40;
uint8_t Concfi_Ina=0x00;


/**
 * Función principal
 */
int main(void){

    ADC1_Init();                                                                    /*  Inicialización del ADC0 */
    SysTick_Init();

    while(1){
        ADC1_PSSI_R |= 0x04;                                                        /*  ADC1 => SS2 -> Begin sampling */
        SysTick_Wait_1ms(2);
        ADC1_PSSI_R |= 0x02;
}}


void Handler_ADC1SS2 (void){
    ADC_result = (ADC1_SSFIFO2_R & 0xFFF);                                      /*  Lectura del resultado de conversión de la primera muestra del secuenciador SS2 */
    temperature = 147.5 - ((75 * (3.3 - 0) * ADC_result) / 4096);               /*  Cálculo de la temperatura del sensor en °C (pp. 1068) */
    ADC1_ISC_R |= 0x0004;
}

void Handler_ADC1SS1 (void){
    ADC_result1 = (ADC1_SSFIFO1_R & 0xFFF);                                      /*  Lectura del resultado de conversión de la primera muestra del secuenciador SS2 */
    ADC_result2 = (ADC1_SSFIFO1_R & 0xFFF);
    ADC_result3 = (ADC1_SSFIFO1_R & 0xFFF);
    ADC1_ISC_R |= 0x0002;
}

