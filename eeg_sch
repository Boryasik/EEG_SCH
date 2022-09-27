import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
import os
from scipy import signal

# Функция для 1 задания. Разделяет сигналы на 16 каналов
def data_sch(name_file_eea):
    f = open(name_file_eea, 'r', encoding='utf8', errors='ignore')
    df = pd.DataFrame(f)
    channel = ['F7', 'F3', 'F4', 'F8', 'T3', 'C3', 'Cz', 'C4', 'T4', 'T5', 'P3', 'Pz', 'P4', 'T6', 'O1', 'O2']
    dfstr = 0
    dfstr2 = 7680
    dfcol = 1
    for i in (channel):
        df.insert(dfcol, i, 0)
        temp = (df.iloc[dfstr:dfstr2][0]).replace(r'\s+', '', regex=True).reset_index(drop=True)
        df.loc[0:7680, i] = temp
        dfstr += 7680
        dfstr2 += 7680
        dfcol += 1
    del df[0]
    df = df.head(7680).astype(float)
    return df

# Функция для 1 задания, сохраняет DataFrame на 16 каналов для каждого испытуемого
def save_data_csv(list_norm, list_sch):

    for i in list_norm:
        df = data_sch("C:\\Program Files\\Python\\New\\1\\venv\\data\\norm\\" + i)
        df.to_csv(r'C:\\Program Files\\Python\\New\\1\\venv\\data\\norm_csv\\' + i.replace('.eea', '') + '.csv', index=False)

    for i in list_sch:
        df = data_sch("C:\\Program Files\\Python\\New\\1\\venv\\data\\sch\\" + i)
        df.to_csv(r'C:\\Program Files\\Python\\New\\1\\venv\\data\\sch_csv\\' + i.replace('.eea', '') + '.csv', index=False)

    return print('files saved')

# Функция для 2 задания, выводит график 16 каналов
def graphics(name_file_eea):
    mkV = np.loadtxt(name_file_eea, unpack=True)
    channel = ['F7', 'F3', 'F4', 'F8', 'T3', 'C3', 'Cz', 'C4', 'T4', 'T5', 'P3', 'Pz', 'P4', 'T6', 'O1', 'O2']
    Y = []
    y = 0
    X = []
    x = 0
    ax = 1
    figure = plt.figure()
    figure.set_size_inches(20, 10)
    for i in range (len(mkV)):
        y = mkV[i]
        Y.append(y)
        x += 1
        X.append(x)
        while x % 7680 == 0:
            globals()['asd' + str(i)] = figure.add_subplot(4, 4, ax)
            globals()['asd' + str(i)].plot(X, Y)
            globals()['asd' + str(i)].set_title(channel[ax-1])
            globals()['asd' + str(i)].set_xlabel("Number of signal")
            globals()['asd' + str(i)].set_ylabel("mkV")
            Y.clear(), X.clear()
            ax += 1
            break
    plt.tight_layout()
    plt.show()

# Функция для 2 задания, сохраняет все графики
def graphics_and_save(file_path, name_file_eea, file_path_save):
    mkV = np.loadtxt(file_path + name_file_eea, unpack=True)
    channel = ['F7', 'F3', 'F4', 'F8', 'T3', 'C3', 'Cz', 'C4', 'T4', 'T5', 'P3', 'Pz', 'P4', 'T6', 'O1', 'O2']
    Y = []
    y = 0
    X = []
    x = 0
    ax = 1
    figure = plt.figure()
    figure.set_size_inches(20, 10)
    for i in range (len(mkV)):
        y = mkV[i]
        Y.append(y)
        x += 1
        X.append(x)
        while x % 7680 == 0:
            globals()['asd' + str(i)] = figure.add_subplot(4, 4, ax)
            globals()['asd' + str(i)].plot(X, Y)
            globals()['asd' + str(i)].set_title(channel[ax-1])
            globals()['asd' + str(i)].set_xlabel("Number of signal")
            globals()['asd' + str(i)].set_ylabel("mkV")
            Y.clear(), X.clear()
            ax += 1
            break
    plt.tight_layout()
    plt.savefig(file_path_save + name_file_eea.replace('.eea', '') + ".png")

# Функция для 3 задания, фильтрация сигналов от помех 50Гц. Возвращает отфильтрованый сигнал
def filter_ffilt(file_path):
    fs = 128.0  # Sample frequency (Hz)
    f0 = 50.0  # Frequency to be removed from signal (Hz)
    Q = 30.0  # Quality factor
    b, a = signal.iirnotch(f0, Q, fs)
    y_for_filtfilt = np.loadtxt(file_path, unpack=True)
    y = signal.filtfilt(b, a, y_for_filtfilt) # отфильтрованый сигнал
    return y

# Функция для 3 задания, фильтрует все значения от помех 50Гц, разделяет на 16 сигналов и выводит графики
def graphics_on_16_signals(value_sheet_mkV, name_file_eea, file_path_save): # подаётся список отфильтрованых значений
    channel = ['F7', 'F3', 'F4', 'F8', 'T3', 'C3', 'Cz', 'C4', 'T4', 'T5', 'P3', 'Pz', 'P4', 'T6', 'O1', 'O2']
    Y = []
    y = 0
    X = []
    x = 0
    ax = 1
    figure = plt.figure()
    figure.set_size_inches(20, 10)
    for i in range (len(value_sheet_mkV)):
        y = value_sheet_mkV[i]
        Y.append(y)
        x += 1
        X.append(x)
        while x % 7680 == 0:
            globals()['asd' + str(i)] = figure.add_subplot(4, 4, ax)
            globals()['asd' + str(i)].plot(X, Y)
            globals()['asd' + str(i)].set_title(channel[ax-1])
            globals()['asd' + str(i)].set_xlabel("Number of signal")
            globals()['asd' + str(i)].set_ylabel("mkV")
            Y.clear(), X.clear()
            ax += 1
            break
    plt.tight_layout()
    plt.savefig(file_path_save + name_file_eea.replace('.eea', '')+"filter.png")
#    plt.show()

# Функция для 4 задания, сохраняет bar амплитуды от диапазонов для 16 каналов
def calculate_psd_save(file_path, file_path_save):
    data_with_files = os.listdir(file_path)

    for i in data_with_files:

        pd_data = pd_data = pd.read_csv(file_path + i, delimiter=',')
        name_column = pd_data.columns  # получаем список имён столбцов

        figure = plt.figure()
        figure.set_size_inches(20, 10)

        fs = 128
        axCOL = 1

        for j in name_column:
            ax = plt.subplot(4, 4, axCOL)
            count_column = pd_data[j].tolist()  # получаем значения столбца
            f, psd = signal.welch(count_column, fs, nperseg=fs)
            Delta = np.average(psd[0:4])
            Theta = np.average(psd[4:7])
            Alpha = np.average(psd[8:13])
            Beta = np.average(psd[14:30])
            Gamma = np.average(psd[30:64])
            Band = ['Delta', 'Theta', 'Alpha', 'Beta', 'Gamma']
            Mean = [Delta, Theta, Alpha, Beta, Gamma]
            plt.title(j)
            ax.bar(Band, Mean)
            ax.set_xlabel("EEG band")
            ax.set_ylabel("Mean band Amplitude")
            axCOL += 1
        plt.tight_layout()
        # plt.show()
        plt.savefig(file_path_save + i.replace('.csv', '') + "psd.png")

# 1
# сохраняем датафреймы по 16 сигналов
path_norm = 'C:\\Program Files\\Python\\New\\1\\venv\\data\\norm\\'
path_sch = 'C:\\Program Files\\Python\\New\\1\\venv\\data\\sch\\'

path_norm_csv = 'C:\\Program Files\\Python\\New\\1\\venv\\data\\norm_csv\\'
path_sch_csv = 'C:\\Program Files\\Python\\New\\1\\venv\\data\\sch_csv\\'

list_norm = os.listdir("""C:\\Program Files\\Python\\New\\1\\venv\\data\\norm""")
list_sch = os.listdir("""C:\\Program Files\\Python\\New\\1\\venv\\data\\sch""")

# save_data_csv(list_norm, list_sch)

# 2
# визуализация и сохранение графиков по каждому испытуемому
file_path_norm_save = "C:\\Program Files\\Python\\New\\1\\venv\\data\\norm_graphics_png\\"
file_path_sch_save = "C:\\Program Files\\Python\\New\\1\\venv\\data\\sch_graphics_png\\"

# for i in list_norm:
#    graphics_and_save(path_norm, i, file_path_norm_save)
# for i in list_sch:
#    graphics_and_save(path_sch, i, file_path_sch_save)

# 3
# сохранение отфильтрованых графиков
file_path_save_filter_norm = "C:\\Program Files\\Python\\New\\1\\venv\\data\\norm_filter_graphic_png\\"
file_path_save_filter_sch = "C:\\Program Files\\Python\\New\\1\\venv\\data\\sch_filter_graphic_png\\"

# for i in list_norm:
#     y = filter_ffilt(path_norm + i)
#     graphics_on_16_signals(y, i, file_path_save_filter_norm)
# for i in list_sch:
#     y = filter_ffilt(path_sch + i)
#     graphics_on_16_signals(y, i, file_path_save_filter_sch)

# 4
# Сохранение графиков диапазонов
file_path_save_psd_norm = "C:\\Program Files\\Python\\New\\1\\venv\\data\\norm_psd_png\\"
file_path_save_psd_sch = "C:\\Program Files\\Python\\New\\1\\venv\\data\\sch_psd_png\\"


# calculate_psd_save(path_norm_csv, file_path_save_psd_norm)
# calculate_psd_save(path_sch_csv, file_path_save_psd_sch)
