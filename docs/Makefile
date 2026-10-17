# Geração dos PDFs dos pontos de controle da documentação do projeto.
# Ao executar apenas "make", mostra a ajuda.
.DEFAULT_GOAL := help

# Requer GNU Make, Pandoc e um mecanismo LaTeX instalado para gerar PDF.

PANDOC ?= pandoc
PANDOC_FLAGS ?= -V geometry:margin=0.8in -V geometry:a4paper

PDFS := PC1.pdf PC2.pdf PC3.pdf PC4.pdf PC5.pdf PC6.pdf

PC1_SOURCES := 1_TAP.md 2_Requisitos.md 3_EAP.md
PC2_SOURCES := 4_1_Projeto_conceitual_de_hardware.md \
               4_2_Projeto_conceitual_de_software.md \
               5_Cronograma.md
PC3_SOURCES := 6_1_Testes_de_hardware.md 6_2_Testes_de_software.md
PC4_SOURCES := 6_3_Testes_de_integração.md
# Mantido conforme o script original: PC4 e PC5 usam o mesmo arquivo.
PC5_SOURCES := 6_3_Testes_de_integração.md
PC6_SOURCES := 7_Relatório_de_encerramento_do_projeto.md

.PHONY: all clean help check-pandoc $(PDFS)

# Verifica se o Pandoc está instalado antes de tentar gerar os PDFs.
check-pandoc:
	@if ! command -v "$(PANDOC)" >/dev/null 2>&1; then \
		echo "Aviso: Pandoc não está instalado. Instale o pandoc executando 'sudo apt update && sudo apt install pandoc'"; \
		exit 1; \
	fi

# Gera todos os PDFs.
all: $(PDFS)

# Cada PDF depende dos arquivos Markdown que o compõem.
# Os alvos PDF são .PHONY para forçar a recompilação mesmo se o PDF existir.
PC1.pdf: $(PC1_SOURCES) | check-pandoc
	$(PANDOC) $(PANDOC_FLAGS) $(PC1_SOURCES) -o "$@"

PC2.pdf: $(PC2_SOURCES) | check-pandoc
	$(PANDOC) $(PANDOC_FLAGS) $(PC2_SOURCES) -o "$@"

PC3.pdf: $(PC3_SOURCES) | check-pandoc
	$(PANDOC) $(PANDOC_FLAGS) -V geometry:landscape $(PC3_SOURCES) -o "$@"

PC4.pdf: $(PC4_SOURCES) | check-pandoc
	$(PANDOC) $(PANDOC_FLAGS) -V geometry:landscape $(PC4_SOURCES) -o "$@"

PC5.pdf: $(PC5_SOURCES) | check-pandoc
	$(PANDOC) $(PANDOC_FLAGS) -V geometry:landscape $(PC5_SOURCES) -o "$@"

PC6.pdf: $(PC6_SOURCES) | check-pandoc
	$(PANDOC) $(PANDOC_FLAGS) $(PC6_SOURCES) -o "$@"

# Remove somente os PDFs gerados por este Makefile.
clean:
	rm -f $(PDFS)

help:
	@echo "Uso:"
	@echo "   make PC1.pdf       Gera o PDF do ponto de controle 1"
	@echo "   make PC2.pdf       Gera o PDF do ponto de controle 2"
	@echo "   make PC3.pdf       Gera o PDF do ponto de controle 3"
	@echo "   make PC4.pdf       Gera o PDF do ponto de controle 4"
	@echo "   make PC5.pdf       Gera o PDF do ponto de controle 5"
	@echo "   make PC6.pdf       Gera o PDF do ponto de controle 6"
	@echo "   make all           Gera todos os PDFs"
	@echo "   make clean         Remove os PDFs gerados"
