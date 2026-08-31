# Plantas vetoriais interativas

Reconstruídas como SVG de verdade: fundo branco, paredes/ambientes em geometria SVG e sem os círculos dos gráficos.

Cada área clicável é um `<g>` com:
- `id`
- `data-area`
- `data-name`
- `tabindex`

Exemplo:
document.querySelector('#lab-alimentos').addEventListener('click', e => {
  console.log(e.currentTarget.dataset.name);
});
