# relogio-slip
relogio para notion
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Relógio Flip Style para Notion</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            background: #1c2526;
            font-family: 'Courier New', Courier, monospace;
            overflow: hidden;
        }
        .relogio-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            background: #000;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
        }
        .time-display {
            display: flex;
            gap: 5px;
        }
        .flap {
            background: #000;
            color: #fff;
            font-size: 4em;
            font-weight: bold;
            width: 80px;
            height: 100px;
            line-height: 100px;
            text-align: center;
            border: 2px solid #333;
            border-radius: 5px;
            position: relative;
            box-shadow: inset 0 0 5px rgba(255, 255, 255, 0.1);
        }
        .flap::before {
            content: '';
            position: absolute;
            top: 50%;
            left: 0;
            width: 100%;
            height: 2px;
            background: #333;
        }
        .colon {
            font-size: 4em;
            color: #fff;
            line-height: 100px;
        }
        .ampm {
            font-size: 1.5em;
            color: #fff;
            position: absolute;
            left: -40px;
            top: 50%;
            transform: translateY(-50%);
        }
        .date-display {
            display: flex;
            gap: 5px;
            margin-top: 10px;
        }
        .date-flap {
            background: #000;
            color: #fff;
            font-size: 1.5em;
            font-weight: bold;
            padding: 5px 15px;
            text-align: center;
            border: 2px solid #333;
            border-radius: 5px;
            text-transform: uppercase;
        }
        @media (max-width: 600px) {
            .flap {
                font-size: 3em;
                width: 60px;
                height: 80px;
                line-height: 80px;
            }
            .colon {
                font-size: 3em;
                line-height: 80px;
            }
            .ampm {
                font-size: 1.2em;
                left: -30px;
            }
            .date-flap {
                font-size: 1.2em;
                padding: 5px 10px;
            }
        }
    </style>
</head>
<body>
    <div class="relogio-container">
        <div class="time-display">
            <div class="ampm" id="ampm"></div>
            <div class="flap" id="hour1"></div>
            <div class="flap" id="hour2"></div>
            <div class="colon">:</div>
            <div class="flap" id="minute1"></div>
            <div class="flap" id="minute2"></div>
        </div>
        <div class="date-display">
            <div class="date-flap" id="dayOfWeek"></div>
            <div class="date-flap" id="dayOfMonth"></div>
            <div class="date-flap" id="month"></div>
        </div>
    </div>
    <script>
        function atualizarRelogio() {
            const agora = new Date();
            const diasSemana = ["Domingo", "Segunda", "Terça", "Quarta", "Quinta", "Sexta", "Sábado"];
            const meses = ["Janeiro", "Fevereiro", "Março", "Abril", "Maio", "Junho", "Julho", "Agosto", "Setembro", "Outubro", "Novembro", "Dezembro"];

            let horas = agora.getHours() % 12;
            horas = horas === 0 ? 12 : horas;
            const minutos = agora.getMinutes();
            const ampm = agora.getHours() >= 12 ? "PM" : "AM";

            const horasStr = horas.toString().padStart(2, '0');
            const minutosStr = minutos.toString().padStart(2, '0');

            const diaSemana = diasSemana[agora.getDay()];
            const dia = agora.getDate().toString().padStart(2, '0');
            const mes = meses[agora.getMonth()];

            document.getElementById('hour1').innerText = horasStr[0];
            document.getElementById('hour2').innerText = horasStr[1];
            document.getElementById('minute1').innerText = minutosStr[0];
            document.getElementById('minute2').innerText = minutosStr[1];
            document.getElementById('ampm').innerText = ampm;
            document.getElementById('dayOfWeek').innerText = diaSemana;
            document.getElementById('dayOfMonth').innerText = dia;
            document.getElementById('month').innerText = mes;
        }

        setInterval(atualizarRelogio, 1000);
        atualizarRelogio();
    </script>
</body>
</html>
