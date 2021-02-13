# module_0
import numpy as np
print("Загадано число от 1 до 100")

def game_guess_number(number):
    '''Определяем нижнюю и верхнею границу диапазона, в котором компьютер будет
    угадывать число пока не достигним правильного результата. Счетчик попыток
    устанавливаем на единицу так как есть вероятность угадать число с первого раза'''
    low_bound = 1
    high_bound = 100
    count = 1
    predict = np.random.randint(1, 101)

    while predict != number:
        count += 1
        if predict > number:
            high_bound = predict
        elif predict < number:
            low_bound = predict + 1
        '''Вычисляем новое значение угадываемого числа в новых границах'''
        predict = (low_bound + high_bound) // 2

    return (count)

def score_game(game_core):
    '''Запускаем игру 1000 раз, чтобы узнать, как быстро игра угадывает число'''
    count_ls = []
    np.random.seed(1)  # фиксируем RANDOM SEED, чтобы ваш эксперимент был воспроизводим!
    random_array = np.random.randint(1, 101, size=(1000))

    for number in random_array:
        count_ls.append(game_core(number))
    score = int(np.mean(count_ls))
    print(f"Ваш алгоритм угадывает число в среднем за {score} попыток")

    return(score)

score_game(game_guess_number)
