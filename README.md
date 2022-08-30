from datetime import datetime


class _No:
    def __init__(self, valor):
        self.valor = valor
        self.proximo = None
        self.anterior = None

    def __str__(self):
        proximo = f', {self.proximo}'
        if self.proximo is None:
            proximo = ''
        return f'{self.valor}{proximo}'


class DoublyLinkedList:
    def __init__(self, tipo=None):
        self.inicio = None
        self.final = None
        self.tamanho = 0
        self.tipo = tipo

    def __str__(self):
        value_list = '['
        perc = self.inicio
        while perc.proximo:
            value_list += f' {perc.valor}, '
            perc = perc.proximo
        value_list += f'{perc.valor} ]'
        return value_list
        # return f'[{self.inicio}]' if self.inicio else '[]'

    def __len__(self):
        return self.tamanho

    def _percorrer(self, perc, count, proximo):
        for i in range(count):
            if proximo:
                perc = perc.proximo
            else:
                perc = perc.anterior
        return perc

    def _get_perc_index(self, index):
        if index >= self.tamanho or index < 0:
            raise IndexError('Não existe esse posição!')
        if index == 0:
            return self.inicio
        elif index == self.tamanho - 1:
            return self.final
        else:
            metade = int(self.tamanho - 1/2)
            count = 0
            proximo = True
            perc = self.inicio
            if index <= metade:
                count = index - 0
            else:
                proximo = False
                count = (self.tamanho - 1) - index
                perc = self.final
            return self._percorrer(perc,count,proximo)

    def buscar_valor_por_index(self,index):
        perc = self._get_perc_index(index)
        return perc.valor
        
    def _get_perc_valor(self, valor):
       pass

    def get_valor(self, index):
        pass

    def get_index(self, valor):
        pass

    def adicionar(self, valor):
        no = _No(valor)
        if self.tamanho == 0:
            self.inicio = no
            self.final = no

        else:
            self.final.proximo = no
            no.anterior = self.final
            self.final = no
        self.tamanho +=1

    def inserir(self, index, valor):
        no = _No(valor)
        if (index == 0):
            no.proximo = self.inicio
            self.inicio.anterior = no
            self.inicio = no
        elif (index ==1):
            temp = self.inicio.proximo
            temp.anterior = no
            no.proximo = temp
            self.inicio.proximo = no
            no.anterior = self.inicio
        else:
            temp = self.inicio
            for i in range(0, index):
                temp =  temp.proximo

            if (temp == None):
                self.adicionar(valor)
            else:
                anterior = temp.anterior
                temp.anterior = no
                no.proximo = temp
                no.anterior = anterior
                anterior.proximo = no


    def editar_item(self, index, novo_valor):
        pass
    def remover_item(self, valor):
        temp = self.inicio
        if (temp):
            if (temp.valor == valor):
                self.inicio = temp.proximo
                return
        while (temp):
            if (temp.valor == valor):
                break
            else:
                temp = temp.proximo
        if (temp == None):
            raise TypeError('Não exite esse valor!')

        anterior = temp.anterior
        anterior.proximo = temp.proximo

    def remover_index(self, index):
        if (index < 1):
            print("\na posição deve ser >= 1.")
        elif (index == 1 and self.inicio != None):
            no = self.inicio
            self.inicio = self.inicio.proximo
            no = None
            if (self.inicio != None):
                self.inicio.anterior = None
        else:
            temp = self.inicio
            for i in range(1, index - 1):
                if (temp != None):
                    temp = temp.proximo
            if (temp != None and temp.proximo != None):
                no = temp.proximo
                temp.proximo = temp.proximo.proximo
                if (temp.proximo.proximo != None):
                    temp.proximo.proximo.anterior = temp.proximo
                no = None
            else:
                print("\nO nó já é nulo.")

    def buscar_valores_repetidos(self):
        pass

    def ordernar(self, crescente=True):
        # insertionSort
        pass
        
        
listadupla = DoublyLinkedList()
listadupla.adicionar(10)
listadupla.adicionar(20)
listadupla.adicionar(30)
listadupla.adicionar(30)
listadupla.adicionar(60)
listadupla.inserir(2, 2)
