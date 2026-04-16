Seccion de programas depositados


_italic text_
1. Suma, resta, multiplicación

.global sub_op
.type sub_op, %function
sub_op:
    sub x0, x0, x1
    ret

.global mul_op
.type mul_op, %function
mul_op:
    mul x0, x0, x1
    ret
    
2. Máximo y mínimo (uso de condiciones)
.global max_op
.type max_op, %function
max_op:
    cmp x0, x1
    csel x0, x0, x1, gt
    ret

.global min_op
.type min_op, %function
min_op:
    cmp x0, x1
    csel x0, x0, x1, lt
    ret

3. Suma de arreglo
   .global sum_array
.type sum_array, %function
sum_array:
    // x0 = ptr
    // x1 = size

    mov x2, #0      // sum
    mov x3, #0      // i

loop_sum:
    cmp x3, x1
    b.ge end_sum

    ldr x4, [x0, x3, lsl #3]
    add x2, x2, x4

    add x3, x3, #1
    b loop_sum

end_sum:
    mov x0, x2
    ret

4. Conteo de pares
   .global count_even
.type count_even, %function
count_even:
    mov x2, #0
    mov x3, #0

loop_even:
    cmp x3, x1
    b.ge end_even

    ldr x4, [x0, x3, lsl #3]
    and x5, x4, #1
    cmp x5, #0
    cinc x2, x2, eq

    add x3, x3, #1
    b loop_even

end_even:
    mov x0, x2
    ret
5. Producto punto
---
  .global dot_product
.type dot_product, %function
dot_product:
    mov x2, #0
    mov x3, #0

loop_dot:
    cmp x3, x2
    b.ge end_dot

    ldr x4, [x0, x3, lsl #3]
    ldr x5, [x1, x3, lsl #3]
    mul x6, x4, x5
    add x2, x2, x6

    add x3, x3, #1
    b loop_dot

end_dot:
    mov x0, x2
    ret
---
