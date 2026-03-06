<!DOCTYPE html>
<html lang="pt-BR">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Formulário - Gestor ZyNapse</title>

    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/sweetalert2@11"></script>

    <style>
        :root {
            --color-bg: #f8fafc;
            --color-surface: #ffffff;
            --color-surface-hover: #f1f5f9;
            --color-border: #e2e8f0;
            --color-text-primary: #1e293b;
            --color-text-secondary: #64748b;
            --color-primary: #ea580c;
            --color-primary-hover: #c2410c;
            --color-primary-text: #ffffff;
            --color-primary-focus-ring: rgba(234, 88, 12, 0.4);
            --transition-speed: 0.3s;
        }

        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--color-bg);
            color: var(--color-text-primary);
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 1rem;
        }

        .form-card {
            background-color: var(--color-surface);
            border-radius: 1rem;
            box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.1), 0 8px 10px -6px rgba(0, 0, 0, 0.1);
            width: 100%;
            max-width: 500px;
            padding: 2.5rem 2rem;
            position: relative;
            overflow: hidden;
        }

        /* Decoration */
        .form-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 6px;
            background: linear-gradient(90deg, #ea580c, #f97316);
        }

        .logo-container {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 0.75rem;
            margin-bottom: 2rem;
        }

        .logo-icon {
            font-size: 2rem;
            color: var(--color-primary);
            filter: drop-shadow(0 4px 6px rgba(234, 88, 12, 0.2));
            animation: float 3s ease-in-out infinite;
        }

        @keyframes float {

            0%,
            100% {
                transform: translateY(0);
            }

            50% {
                transform: translateY(-5px);
            }
        }

        .logo-text {
            font-size: 1.5rem;
            font-weight: 800;
            color: var(--color-text-primary);
            letter-spacing: -0.025em;
        }

        .logo-highlight {
            color: var(--color-primary);
        }

        .form-label {
            display: block;
            font-weight: 600;
            color: var(--color-text-secondary);
            margin-bottom: 0.5rem;
            font-size: 0.875rem;
        }

        .form-input {
            display: block;
            background-color: var(--color-bg);
            border: 1px solid var(--color-border);
            color: var(--color-text-primary);
            border-radius: 0.75rem;
            transition: all var(--transition-speed);
            padding: 0.75rem 1rem;
            width: 100%;
            font-size: 1rem;
        }

        .form-input:focus {
            border-color: var(--color-primary);
            box-shadow: 0 0 0 4px var(--color-primary-focus-ring);
            outline: none;
            background-color: var(--color-surface);
        }

        .form-input:disabled,
        .form-input[readonly] {
            background-color: var(--color-surface-hover);
            cursor: not-allowed;
            opacity: 0.8;
            color: var(--color-text-secondary);
        }

        .btn-primary {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            background-color: var(--color-primary);
            color: var(--color-primary-text);
            padding: 0.875rem 1.5rem;
            font-weight: 700;
            border-radius: 0.75rem;
            border: none;
            transition: all var(--transition-speed) ease;
            font-size: 1rem;
            width: 100%;
            cursor: pointer;
            box-shadow: 0 4px 6px -1px rgba(234, 88, 12, 0.3), 0 2px 4px -2px rgba(234, 88, 12, 0.3);
        }

        .btn-primary:hover {
            background-color: var(--color-primary-hover);
            transform: translateY(-2px);
            box-shadow: 0 10px 15px -3px rgba(234, 88, 12, 0.4), 0 4px 6px -4px rgba(234, 88, 12, 0.4);
        }

        .btn-primary:active {
            transform: translateY(0);
        }

        .btn-primary:disabled {
            opacity: 0.7;
            cursor: not-allowed;
            transform: none;
        }

        .input-group {
            position: relative;
            margin-bottom: 1.5rem;
        }

        .input-icon {
            position: absolute;
            right: 1.25rem;
            top: 50%;
            transform: translateY(-50%);
            color: var(--color-text-secondary);
            pointer-events: none;
            transition: color var(--transition-speed);
        }

        .form-input:focus+.input-icon {
            color: var(--color-primary);
        }

        .spinner {
            position: absolute;
            right: 1.25rem;
            top: 50%;
            transform: translateY(-50%);
            color: var(--color-primary);
            display: none;
        }

        .spinner.active {
            display: block;
        }
    </style>
</head>

<body>

    <div class="form-card">
        <header class="logo-container">
            <i class="fa-solid fa-chart-line logo-icon"></i>
            <h1 class="logo-text"><span class="logo-highlight">Gestor</span> ZyNapse</h1>
        </header>

        <p class="text-center text-[var(--color-text-secondary)] mb-6 text-sm">
            Preencha os dados abaixo. Ao digitar o CNPJ, a Razão Social será preenchida automaticamente.
        </p>

        <form id="modelo-form" novalidate>
            <div class="input-group">
                <label for="nome" class="form-label">Nome Completo</label>
                <div class="relative">
                    <input type="text" id="nome" name="nome" class="form-input" placeholder="Digite seu nome" required>
                    <i class="fa-regular fa-user input-icon"></i>
                </div>
            </div>

            <div class="input-group">
                <label for="cnpj" class="form-label">CNPJ</label>
                <div class="relative">
                    <input type="text" id="cnpj" name="cnpj" class="form-input" placeholder="00.000.000/0000-00"
                        required>
                    <i class="fa-solid fa-building input-icon" id="cnpj-icon"></i>
                    <i class="fa-solid fa-circle-notch fa-spin spinner" id="cnpj-spinner"></i>
                </div>
            </div>

            <div class="input-group">
                <label for="razao_social" class="form-label">Razão Social</label>
                <input type="text" id="razao_social" name="razao_social" class="form-input"
                    placeholder="Preenchimento automático" readonly>
            </div>

            <div class="input-group">
                <label for="whatsapp" class="form-label">WhatsApp</label>
                <div class="relative">
                    <input type="tel" id="whatsapp" name="whatsapp" class="form-input" placeholder="(00) 00000-0000"
                        required>
                    <i class="fa-brands fa-whatsapp input-icon" style="color: #25D366; font-size: 1.1rem;"></i>
                </div>
            </div>

            <button type="submit" class="btn-primary mt-4" id="btn-enviar">
                <i class="fa-solid fa-paper-plane mr-2"></i> Enviar Dados
            </button>
        </form>
    </div>

    <script>
        const App = {
            ui: {},

            init() {
                this.cacheUI();
                this.setupEventListeners();
            },

            cacheUI() {
                this.ui = {
                    form: document.getElementById('modelo-form'),
                    nome: document.getElementById('nome'),
                    cnpj: document.getElementById('cnpj'),
                    razaoSocial: document.getElementById('razao_social'),
                    whatsapp: document.getElementById('whatsapp'),
                    cnpjSpinner: document.getElementById('cnpj-spinner'),
                    cnpjIcon: document.getElementById('cnpj-icon'),
                    btnEnviar: document.getElementById('btn-enviar')
                };
            },

            setupEventListeners() {
                // Máscaras
                this.ui.cnpj.addEventListener('input', (e) => this.helpers.applyMask(e, this.helpers.formatCNPJ));
                this.ui.whatsapp.addEventListener('input', (e) => this.helpers.applyMask(e, this.helpers.formatPhone));

                // Busca Automática do CNPJ ao sair do campo (blur)
                this.ui.cnpj.addEventListener('blur', () => this.handlers.onCnpjBlur());

                // Envio do formulário (Apenas Modelo)
                this.ui.form.addEventListener('submit', (e) => this.handlers.onSubmit(e));
            },

            handlers: {
                async onCnpjBlur() {
                    const cnpjValue = App.ui.cnpj.value.replace(/\D/g, '');

                    if (cnpjValue.length !== 14) {
                        return; // Ocultar spinner silenciosamente se não tiver o tamanho certo, sem apagar obrigatoriamente
                    }

                    // Layout Toggle spinner
                    App.ui.cnpjIcon.style.display = 'none';
                    App.ui.cnpjSpinner.classList.add('active');

                    try {
                        const data = await App.api.fetchCNPJData(cnpjValue);
                        if (data && data.razao_social) {
                            App.ui.razaoSocial.value = data.razao_social;

                            Swal.fire({
                                toast: true,
                                position: 'top-end',
                                icon: 'success',
                                title: 'CNPJ preenchido!',
                                showConfirmButton: false,
                                timer: 2000,
                                timerProgressBar: true
                            });
                        } else {
                            App.ui.razaoSocial.value = '';
                            Swal.fire({
                                toast: true,
                                position: 'top-end',
                                icon: 'error',
                                title: 'CNPJ inválido ou não encontrado.',
                                showConfirmButton: false,
                                timer: 3000
                            });
                        }
                    } catch (error) {
                        console.error('Erro ao buscar CNPJ:', error);
                        App.ui.razaoSocial.value = '';
                    } finally {
                        App.ui.cnpjIcon.style.display = 'block';
                        App.ui.cnpjSpinner.classList.remove('active');
                    }
                },

                onSubmit(e) {
                    e.preventDefault();

                    if (!App.ui.form.checkValidity()) {
                        App.ui.form.reportValidity();
                        return;
                    }

                    // Apenas como modelo
                    const btn = App.ui.btnEnviar;
                    const originalHtml = btn.innerHTML;

                    btn.disabled = true;
                    btn.innerHTML = '<i class="fa-solid fa-circle-notch fa-spin mr-2"></i> Processando...';

                    setTimeout(() => {
                        btn.disabled = false;
                        btn.innerHTML = originalHtml;

                        Swal.fire({
                            title: 'Sucesso!',
                            text: 'Este é apenas um modelo. Os dados não foram enviados para nenhum servidor.',
                            icon: 'success',
                            confirmButtonColor: '#ea580c'
                        });

                    }, 1000);
                }
            },

            api: {
                async fetchCNPJData(cnpj) {
                    const response = await fetch(`https://brasilapi.com.br/api/cnpj/v1/${cnpj}`);
                    if (!response.ok) return null;
                    return response.json();
                }
            },

            helpers: {
                formatCNPJ: (v) => {
                    return v.replace(/\D/g, '')
                        .slice(0, 14)
                        .replace(/^(\d{2})(\d)/, '$1.$2')
                        .replace(/^(\d{2})\.(\d{3})(\d)/, '$1.$2.$3')
                        .replace(/\.(\d{3})(\d)/, '.$1/$2')
                        .replace(/(\d{4})(\d)/, '$1-$2');
                },
                formatPhone: (v = '') => {
                    let r = v.replace(/\D/g, '').slice(0, 11);
                    if (r.length > 10) {
                        r = r.replace(/^(\d\d)(\d{5})(\d{4}).*/, '($1) $2-$3');
                    } else if (r.length > 5) {
                        r = r.replace(/^(\d\d)(\d{4})(\d{0,4}).*/, '($1) $2-$3');
                    } else {
                        r = r.replace(/^(\d*)/, '($1)');
                    }
                    return r;
                },
                applyMask: (e, formatter) => {
                    e.target.value = formatter(e.target.value);
                }
            }
        };

        document.addEventListener('DOMContentLoaded', () => App.init());
    </script>
</body>

</html>
