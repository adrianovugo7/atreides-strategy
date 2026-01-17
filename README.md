<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AtreidesStrategy - Painel de Investimentos</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary-color: #0a1f0a;
            --secondary-color: #1a472a;
            --accent-color: #2a623d;
            --light-color: #f8f9fa;
            --dark-color: #2d3748;
            --text-light: #ffffff;
            --text-dark: #2d3748;
            --card-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            --hover-shadow: 0 10px 15px rgba(0, 0, 0, 0.15);
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
            color: var(--text-dark);
            min-height: 100vh;
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 0 20px;
        }
        
        header {
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: var(--text-light);
            padding: 15px 0;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
            position: sticky;
            top: 0;
            z-index: 100;
        }
        
        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .logo-container {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .logo {
            width: 50px;
            height: 50px;
            background: linear-gradient(135deg, #ffffff, #e8f5e8);
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            font-size: 20px;
            color: var(--primary-color);
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
        }
        
        .logo-text h1 {
            font-size: 24px;
            font-weight: 700;
            background: linear-gradient(135deg, #ffffff, #e8f5e8);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 2px;
        }
        
        .logo-text p {
            font-size: 12px;
            opacity: 0.9;
            color: #e8f5e8;
        }
        
        nav ul {
            display: flex;
            list-style: none;
            gap: 5px;
        }
        
        nav ul li a {
            color: var(--text-light);
            text-decoration: none;
            font-weight: 500;
            padding: 8px 16px;
            border-radius: 6px;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            gap: 5px;
        }
        
        nav ul li a:hover, nav ul li a.active {
            background-color: rgba(255, 255, 255, 0.15);
            transform: translateY(-2px);
        }
        
        .social-links {
            display: flex;
            gap: 12px;
        }
        
        .social-links a {
            color: var(--text-light);
            font-size: 18px;
            transition: all 0.3s ease;
            width: 36px;
            height: 36px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            background: rgba(255, 255, 255, 0.1);
        }
        
        .social-links a.youtube:hover {
            background-color: rgba(255, 0, 0, 0.8);
            color: white;
        }
        
        .social-links a.instagram:hover {
            background: radial-gradient(circle at 30% 107%, #fdf497 0%, #fdf497 5%, #fd5949 45%, #d6249f 60%, #285AEB 90%);
            color: white;
        }
        
        .social-links a:hover {
            transform: translateY(-3px);
        }
        
        .youtube-icon {
            color: #ff0000;
        }
        
        .instagram-icon {
            color: #e1306c;
        }
        
        .dashboard {
            padding: 30px 0;
        }
        
        .dashboard-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
        }
        
        .dashboard-title h2 {
            font-size: 28px;
            color: var(--primary-color);
            margin-bottom: 5px;
        }
        
        .dashboard-title p {
            color: #718096;
            font-size: 16px;
        }
        
        .date-filter select {
            padding: 10px 15px;
            border: 1px solid #e2e8f0;
            border-radius: 8px;
            background-color: white;
            font-size: 14px;
            color: var(--dark-color);
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
            cursor: pointer;
        }
        
        .cards {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 24px;
            margin-bottom: 40px;
        }
        
        .card {
            background: linear-gradient(135deg, #ffffff 0%, #f8f9fa 100%);
            border-radius: 12px;
            padding: 24px;
            box-shadow: var(--card-shadow);
            transition: all 0.3s ease;
            border: 1px solid rgba(0, 0, 0, 0.05);
            position: relative;
            overflow: hidden;
        }
        
        .card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 4px;
            background: linear-gradient(90deg, var(--primary-color), var(--secondary-color));
        }
        
        .card:hover {
            transform: translateY(-5px);
            box-shadow: var(--hover-shadow);
        }
        
        .card-title {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }
        
        .card-title h3 {
            font-size: 16px;
            color: #718096;
            font-weight: 600;
        }
        
        .card-icon {
            width: 40px;
            height: 40px;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 18px;
            background: rgba(26, 71, 42, 0.1);
            color: var(--primary-color);
        }
        
        .card-value {
            font-size: 28px;
            font-weight: 700;
            color: var(--primary-color);
            margin-bottom: 5px;
        }
        
        .card-change {
            display: flex;
            align-items: center;
            font-size: 14px;
            font-weight: 600;
        }
        
        .positive {
            color: #38a169;
        }
        
        .negative {
            color: #e53e3e;
        }
        
        .charts {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(500px, 1fr));
            gap: 30px;
            margin-bottom: 40px;
        }
        
        .chart-container {
            background: white;
            border-radius: 12px;
            padding: 24px;
            box-shadow: var(--card-shadow);
            transition: all 0.3s ease;
        }
        
        .chart-container:hover {
            box-shadow: var(--hover-shadow);
        }
        
        .chart-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        
        .chart-header h3 {
            font-size: 18px;
            color: var(--primary-color);
            font-weight: 600;
        }
        
        .chart-actions {
            display: flex;
            gap: 10px;
        }
        
        .chart-actions button {
            background: none;
            border: none;
            color: #a0aec0;
            cursor: pointer;
            font-size: 16px;
            transition: color 0.3s;
        }
        
        .chart-actions button:hover {
            color: var(--primary-color);
        }
        
        .chart-wrapper {
            position: relative;
            height: 300px;
        }
        
        footer {
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: var(--text-light);
            padding: 40px 0 20px;
            margin-top: 60px;
        }
        
        .footer-content {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 24px;
        }
        
        .footer-logo {
            display: flex;
            align-items: center;
            gap: 12px;
            margin-bottom: 10px;
        }
        
        .footer-logo .logo {
            width: 40px;
            height: 40px;
            font-size: 16px;
        }
        
        .footer-logo h3 {
            font-size: 20px;
            background: linear-gradient(135deg, #ffffff, #e8f5e8);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        
        .footer-social {
            display: flex;
            gap: 20px;
            margin: 15px 0;
        }
        
        .footer-social a {
            color: var(--text-light);
            font-size: 20px;
            transition: all 0.3s ease;
            width: 44px;
            height: 44px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            background: rgba(255, 255, 255, 0.1);
        }
        
        .footer-social a.youtube {
            background-color: rgba(255, 0, 0, 0.8);
        }
        
        .footer-social a.instagram {
            background: radial-gradient(circle at 30% 107%, #fdf497 0%, #fdf497 5%, #fd5949 45%, #d6249f 60%, #285AEB 90%);
        }
        
        .footer-social a:hover {
            transform: translateY(-3px);
            opacity: 0.9;
        }
        
        .footer-links {
            display: flex;
            gap: 30px;
            margin-top: 20px;
            flex-wrap: wrap;
            justify-content: center;
        }
        
        .footer-links a {
            color: var(--text-light);
            text-decoration: none;
            transition: opacity 0.3s;
            font-size: 14px;
        }
        
        .footer-links a:hover {
            opacity: 0.8;
        }
        
        .copyright {
            margin-top: 30px;
            font-size: 14px;
            opacity: 0.8;
            text-align: center;
        }
        
        .mobile-menu-btn {
            display: none;
            background: none;
            border: none;
            color: white;
            font-size: 24px;
            cursor: pointer;
        }
        
        @media (max-width: 1200px) {
            .charts {
                grid-template-columns: 1fr;
            }
            
            .chart-wrapper {
                height: 280px;
            }
        }
        
        @media (max-width: 768px) {
            .header-content {
                flex-wrap: wrap;
            }
            
            .mobile-menu-btn {
                display: block;
            }
            
            nav {
                width: 100%;
                order: 3;
                margin-top: 15px;
                display: none;
            }
            
            nav.active {
                display: block;
            }
            
            nav ul {
                flex-direction: column;
                gap: 10px;
            }
            
            .social-links {
                margin-left: auto;
            }
            
            .dashboard-header {
                flex-direction: column;
                align-items: flex-start;
                gap: 15px;
            }
            
            .cards {
                grid-template-columns: 1fr;
            }
            
            .chart-wrapper {
                height: 250px;
            }
            
            .footer-links {
                flex-direction: column;
                gap: 15px;
                align-items: center;
            }
        }
        
        @media (max-width: 480px) {
            .container {
                padding: 0 15px;
            }
            
            .logo-text h1 {
                font-size: 20px;
            }
            
            .card {
                padding: 20px;
            }
            
            .card-value {
                font-size: 24px;
            }
            
            .chart-container {
                padding: 20px;
            }
            
            .chart-wrapper {
                height: 220px;
            }
        }
    </style>
</head>
<body>
    <header>
        <div class="container">
            <div class="header-content">
                <div class="logo-container">
                    <div class="logo">AS</div>
                    <div class="logo-text">
                        <h1>AtreidesStrategy</h1>
                        <p>Investimentos Inteligentes</p>
                    </div>
                </div>
                
                <button class="mobile-menu-btn">
                    <i class="fas fa-bars"></i>
                </button>
                
                <nav id="main-nav">
                    <ul>
                        <li><a href="#" class="active"><i class="fas fa-chart-line"></i> Dashboard</a></li>
                        <li><a href="#"><i class="fas fa-hand-holding-usd"></i> Investimentos</a></li>
                        <li><a href="#"><i class="fas fa-tractor"></i> Agronegócio</a></li>
                        <li><a href="#"><i class="fas fa-file-alt"></i> Relatórios</a></li>
                        <li><a href="#"><i class="fas fa-envelope"></i> Contato</a></li>
                    </ul>
                </nav>
                
                <div class="social-links">
                    <a href="https://youtube.com/@atreides_strategy?si=YmtXGQ37H6339GvG" target="_blank" title="YouTube" class="youtube">
                        <i class="fab fa-youtube youtube-icon"></i>
                    </a>
                    <a href="https://www.instagram.com/atreides_estrategy?igsh=MXY1ZHN3YTJyZXB6OA==" target="_blank" title="Instagram" class="instagram">
                        <i class="fab fa-instagram instagram-icon"></i>
                    </a>
                </div>
            </div>
        </div>
    </header>
    
    <div class="container">
        <section class="dashboard">
            <div class="dashboard-header">
                <div class="dashboard-title">
                    <h2>Painel de Investimentos</h2>
                    <p>Visão geral dos investimentos e desempenho do portfólio</p>
                </div>
                <div class="date-filter">
                    <select id="period-select">
                        <option value="7d">Últimos 7 dias</option>
                        <option value="30d" selected>Últimos 30 dias</option>
                        <option value="90d">Últimos 90 dias</option>
                        <option value="1y">Último ano</option>
                    </select>
                </div>
            </div>
            
            <div class="cards">
                <div class="card">
                    <div class="card-title">
                        <h3>Valor do Portfólio</h3>
                        <div class="card-icon">
                            <i class="fas fa-chart-line"></i>
                        </div>
                    </div>
                    <div class="card-value">R$ 12.458.320</div>
                    <div class="card-change positive">
                        <i class="fas fa-arrow-up"></i> +3.2% (R$ 385.420)
                    </div>
                </div>
                
                <div class="card">
                    <div class="card-title">
                        <h3>CDB + CDI</h3>
                        <div class="card-icon">
                            <i class="fas fa-university"></i>
                        </div>
                    </div>
                    <div class="card-value">R$ 4.250.000</div>
                    <div class="card-change positive">
                        <i class="fas fa-arrow-up"></i> +1.8% (R$ 75.200)
                    </div>
                </div>
                
                <div class="card">
                    <div class="card-title">
                        <h3>Terras & Fazendas</h3>
                        <div class="card-icon">
                            <i class="fas fa-tractor"></i>
                        </div>
                    </div>
                    <div class="card-value">R$ 5.780.000</div>
                    <div class="card-change positive">
                        <i class="fas fa-arrow-up"></i> +4.5% (R$ 248.900)
                    </div>
                </div>
                
                <div class="card">
                    <div class="card-title">
                        <h3>Agronegócio</h3>
                        <div class="card-icon">
                            <i class="fas fa-seedling"></i>
                        </div>
                    </div>
                    <div class="card-value">R$ 2.428.320</div>
                    <div class="card-change positive">
                        <i class="fas fa-arrow-up"></i> +2.7% (R$ 63.320)
                    </div>
                </div>
            </div>
            
            <div class="charts">
                <div class="chart-container">
                    <div class="chart-header">
                        <h3>Performance CDB vs CDI</h3>
                        <div class="chart-actions">
                            <button title="Download"><i class="fas fa-download"></i></button>
                            <button title="Expandir"><i class="fas fa-expand"></i></button>
                        </div>
                    </div>
                    <div class="chart-wrapper">
                        <canvas id="cdbCdiChart"></canvas>
                    </div>
                </div>
                
                <div class="chart-container">
                    <div class="chart-header">
                        <h3>Investimento em Terras e Fazendas</h3>
                        <div class="chart-actions">
                            <button title="Download"><i class="fas fa-download"></i></button>
                            <button title="Expandir"><i class="fas fa-expand"></i></button>
                        </div>
                    </div>
                    <div class="chart-wrapper">
                        <canvas id="landInvestmentChart"></canvas>
                    </div>
                </div>
                
                <div class="chart-container">
                    <div class="chart-header">
                        <h3>Distribuição de Investimentos no Agronegócio</h3>
                        <div class="chart-actions">
                            <button title="Download"><i class="fas fa-download"></i></button>
                            <button title="Expandir"><i class="fas fa-expand"></i></button>
                        </div>
                    </div>
                    <div class="chart-wrapper">
                        <canvas id="agroDistributionChart"></canvas>
                    </div>
                </div>
                
                <div class="chart-container">
                    <div class="chart-header">
                        <h3>Rentabilidade por Segmento</h3>
                        <div class="chart-actions">
                            <button title="Download"><i class="fas fa-download"></i></button>
                            <button title="Expandir"><i class="fas fa-expand"></i></button>
                        </div>
                    </div>
                    <div class="chart-wrapper">
                        <canvas id="profitabilityChart"></canvas>
                    </div>
                </div>
            </div>
        </section>
    </div>
    
    <footer>
        <div class="container">
            <div class="footer-content">
                <div class="footer-logo">
                    <div class="logo">AS</div>
                    <h3>AtreidesStrategy</h3>
                </div>
                
                <p>Investimentos inteligentes para um futuro próspero</p>
                
                <div class="footer-social">
                    <a href="https://youtube.com/@atreides_strategy?si=YmtXGQ37H6339GvG" target="_blank" title="YouTube" class="youtube">
                        <i class="fab fa-youtube"></i>
                    </a>
                    <a href="https://www.instagram.com/atreides_estrategy?igsh=MXY1ZHN3YTJyZXB6OA==" target="_blank" title="Instagram" class="instagram">
                        <i class="fab fa-instagram"></i>
                    </a>
                </div>
                
                <div class="footer-links">
                    <a href="#">Home</a>
                    <a href="#">Sobre Nós</a>
                    <a href="#">Serviços</a>
                    <a href="#">Investimentos</a>
                    <a href="#">Contato</a>
                </div>
                
                <div class="copyright">
                    &copy; 2023 AtreidesStrategy. Todos os direitos reservados.
                </div>
            </div>
        </div>
    </footer>

    <script>
        // Menu mobile
        document.querySelector('.mobile-menu-btn').addEventListener('click', function() {
            document.getElementById('main-nav').classList.toggle('active');
        });
        
        // Dados dos gráficos
        const months = ['Jan', 'Fev', 'Mar', 'Abr', 'Mai', 'Jun', 'Jul', 'Ago', 'Set', 'Out', 'Nov', 'Dez'];
        const regions = ['Centro-Oeste', 'Sudeste', 'Sul', 'Norte', 'Nordeste'];
        const agroSegments = ['Grãos', 'Bovinos', 'Equinos', 'Florestas', 'Outros'];
        
        // Gerar dados aleatórios
        const generateData = (points, startValue, volatility, trend = 0) => {
            const data = [];
            let value = startValue;
            for (let i = 0; i < points; i++) {
                value = value * (1 + (Math.random() * volatility * 2 - volatility) + trend);
                data.push(value);
            }
            return data;
        };
        
        // Gráfico 1: CDB vs CDI
        new Chart(document.getElementById('cdbCdiChart'), {
            type: 'line',
            data: {
                labels: months,
                datasets: [
                    {
                        label: 'CDB',
                        data: generateData(12, 1000000, 0.02, 0.005),
                        borderColor: '#0a1f0a',
                        backgroundColor: 'rgba(10, 31, 10, 0.1)',
                        tension: 0.3,
                        fill: true,
                        borderWidth: 2
                    },
                    {
                        label: 'CDI',
                        data: generateData(12, 1000000, 0.015, 0.003),
                        borderColor: '#1a472a',
                        backgroundColor: 'rgba(26, 71, 42, 0.1)',
                        tension: 0.3,
                        fill: true,
                        borderWidth: 2
                    }
                ]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: { 
                        position: 'top',
                        labels: {
                            usePointStyle: true,
                            padding: 15
                        }
                    },
                    tooltip: {
                        mode: 'index',
                        intersect: false,
                        callbacks: {
                            label: function(context) {
                                return context.dataset.label + ': R$ ' + context.parsed.y.toLocaleString('pt-BR');
                            }
                        }
                    }
                },
                scales: {
                    y: {
                        beginAtZero: false,
                        grid: {
                            color: 'rgba(0, 0, 0, 0.05)'
                        },
                        ticks: {
                            callback: function(value) {
                                return 'R$ ' + (value / 1000).toFixed(0) + 'K';
                            }
                        }
                    },
                    x: {
                        grid: {
                            color: 'rgba(0, 0, 0, 0.05)'
                        }
                    }
                }
            }
        });
        
        // Gráfico 2: Investimento em Terras
        new Chart(document.getElementById('landInvestmentChart'), {
            type: 'bar',
            data: {
                labels: regions,
                datasets: [{
                    label: 'Valor Investido (R$)',
                    data: [1850000, 1520000, 980000, 750000, 680000],
                    backgroundColor: [
                        'rgba(10, 31, 10, 0.8)',
                        'rgba(26, 71, 42, 0.8)',
                        'rgba(42, 98, 61, 0.8)',
                        'rgba(93, 140, 90, 0.8)',
                        'rgba(139, 175, 117, 0.8)'
                    ],
                    borderColor: [
                        'rgb(10, 31, 10)',
                        'rgb(26, 71, 42)',
                        'rgb(42, 98, 61)',
                        'rgb(93, 140, 90)',
                        'rgb(139, 175, 117)'
                    ],
                    borderWidth: 1,
                    borderRadius: 5
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: { 
                        display: false
                    },
                    tooltip: {
                        callbacks: {
                            label: function(context) {
                                return 'Valor: R$ ' + context.parsed.y.toLocaleString('pt-BR');
                            }
                        }
                    }
                },
                scales: {
                    y: {
                        beginAtZero: true,
                        grid: {
                            color: 'rgba(0, 0, 0, 0.05)'
                        },
                        ticks: {
                            callback: function(value) {
                                return 'R$ ' + (value / 1000).toFixed(0) + 'K';
                            }
                        }
                    },
                    x: {
                        grid: {
                            display: false
                        }
                    }
                }
            }
        });
        
        // Gráfico 3: Distribuição do Agronegócio
        new Chart(document.getElementById('agroDistributionChart'), {
            type: 'doughnut',
            data: {
                labels: agroSegments,
                datasets: [{
                    data: [45, 25, 15, 10, 5],
                    backgroundColor: [
                        'rgba(10, 31, 10, 0.8)',
                        'rgba(26, 71, 42, 0.8)',
                        'rgba(42, 98, 61, 0.8)',
                        'rgba(93, 140, 90, 0.8)',
                        'rgba(139, 175, 117, 0.8)'
                    ],
                    borderWidth: 1,
                    hoverOffset: 15
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: { 
                        position: 'right',
                        labels: {
                            usePointStyle: true,
                            padding: 15
                        }
                    },
                    tooltip: {
                        callbacks: {
                            label: function(context) {
                                return context.label + ': ' + context.parsed + '%';
                            }
                        }
                    }
                }
            }
        });
        
        // Gráfico 4: Rentabilidade por Segmento
        new Chart(document.getElementById('profitabilityChart'), {
            type: 'bar',
            data: {
                labels: ['CDB/CDI', 'Terras', 'Grãos', 'Bovinos', 'Equinos'],
                datasets: [{
                    label: 'Rentabilidade (%)',
                    data: [4.2, 6.8, 8.5, 7.2, 5.9],
                    backgroundColor: 'rgba(10, 31, 10, 0.8)',
                    borderColor: 'rgb(10, 31, 10)',
                    borderWidth: 1,
                    borderRadius: 5
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: { 
                        display: false
                    },
                    tooltip: {
                        callbacks: {
                            label: function(context) {
                                return 'Rentabilidade: ' + context.parsed.y + '%';
                            }
                        }
                    }
                },
                scales: {
                    y: {
                        beginAtZero: true,
                        grid: {
                            color: 'rgba(0, 0, 0, 0.05)'
                        },
                        ticks: {
                            callback: function(value) {
                                return value + '%';
                            }
                        }
                    },
                    x: {
                        grid: {
                            display: false
                        }
                    }
                }
            }
        });
        
        // Filtro de período
        document.getElementById('period-select').addEventListener('change', function() {
            console.log('Período alterado para: ' + this.options[this.selectedIndex].text);
        });
    </script>
</body>
</html>
