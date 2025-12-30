# CAPTCHA Solver  

[![Promo](https://github.com/luminati-io/LinkedIn-Scraper/raw/main/Proxies%20and%20scrapers%20GitHub%20bonus%20banner.png)](https://brightdata.jp/) 

[Bright Data's CAPTCHA Solver](https://brightdata.jp/products/web-unlocker/captcha-solver) を使用すると、ユーザーエミュレーション、フィンガープリント管理、強力なプロキシインフラストラクチャにより、reCAPTCHA、hCaptcha、PX Captcha、GeeTest などの CAPTCHA を簡単に解決できます。  
当社の CAPTCHA Solver は、[Scraping Browser](https://brightdata.jp/products/scraping-browser) および [Web Unlocker](https://brightdata.jp/products/web-unlocker) の組み込み機能です。

カスタム CDP 関数の詳細は[こちら](https://docs.brightdata.com/scraping-automation/scraping-browser/cdp-functions/custom#captcha-solver)をご覧ください。


## Features  

- 高速かつ自動化された CAPTCHA 解決  
- reCAPTCHA、hCaptcha、PX Captcha、GeeTest、SimpleCaptcha などに対応  
- 検知回避のためのインテリジェントなユーザーエミュレーションとフィンガープリンティング  
- 受賞歴のある [100M+ IPs のプロキシネットワーク](https://brightdata.jp/proxy-types) を活用  
- 99.9% の稼働率と 24/7 サポートで、結果に対してのみお支払い  



## Why Choose CAPTCHA Solver  

- **世界中で 20,000+ のお客様に信頼されています**  
- **開発者向けに構築されています**  
  - AI 駆動のアンロックロジック  
  - 自動 CAPTCHA 解決とリトライ  
  - JavaScript レンダリングを内蔵  
  - Puppeteer、Playwright、Selenium などのツールと簡単に統合可能
 
 > **📚 Webスクレイピングの詳細はこちら:**
 >> [**Puppeteer**](https://brightdata.jp/blog/how-tos/web-scraping-puppeteer)<br>
 >> [**Playwright**](https://brightdata.jp/blog/how-tos/playwright-web-scraping)<br>
 >> [**Selenium**](https://brightdata.jp/blog/how-tos/using-selenium-for-web-scraping)

- **比類ない信頼性**  
  - 99.9% の成功率  
  - 4 年以上の R&D と 80+ 名の専任エンジニア  
  - 年間 5.5 兆件以上のデータリクエストを処理  



# How CAPTCHA Solver Works  

Bright Data の CAPTCHA Solver は **Scraping Browser** と **Web Unlocker** に統合されており、デフォルトで **CAPTCHA を自動的に解決** します。以下が可能です:  

- コード内で解決プロセスを監視する  
- Chrome DevTools Protocol (CDP) コマンドを使用して CAPTCHA 解決の挙動を手動で切り替える  
- 必要に応じて CAPTCHA 解決を完全に無効化する  



## **Automatic CAPTCHA Solving**  

`Captcha.solve` コマンドを使用して CAPTCHA を検知し、自動的に解決します。Python 版は[こちら](https://docs.brightdata.com/scraping-automation/scraping-browser/cdp-functions/custom#captcha-solver)で確認できます。

### Command Overview  

```javascript
Captcha.solve({
    detectTimeout?: number // Timeout for CAPTCHA detection in milliseconds  
    options?: CaptchaOptions[] // Configuration options for CAPTCHA solving  
}) : SolveResult
```

### Example: NodeJS (Puppeteer)

```javascript
(async () => {
  const page = await browser.newPage();
  const client = await page.target().createCDPSession();
  await page.goto('https://site-with-captcha.com');
  try {
    // Automatically solve CAPTCHA  
    const { status } = await client.send('Captcha.solve', { detectTimeout: 30000 });
    console.log(`CAPTCHA solve status: ${status}`);
  } catch (error) {
    console.error('Error solving CAPTCHA:', error);
  }
})();
```

### Events Monitoring  

高度なユースケースに対応するために、特定の CAPTCHA 解決イベントをリッスンできます:  

- **`Captcha.detected`**: CAPTCHA が検知され、解決が開始されました  
- **`Captcha.solveFinished`**: CAPTCHA が正常に解決されました  
- **`Captcha.solveFailed`**: CAPTCHA の解決に失敗しました  
- **`Captcha.waitForSolve`**: CAPTCHA Solver の完了待ちです  

#### NodeJS Example - Listening for Events

```javascript
const client = await page.target().createCDPSession();
await new Promise((resolve, reject) => {
  client.on('Captcha.solveFinished', (result) => {
    if (result.status === 'success') {
      resolve();
    } else {
      reject(new Error('CAPTCHA solving failed with status: ' + result.status));
    }
  });
  client.on('Captcha.solveFailed', () => reject(new Error('CAPTCHA solving failed')));
  setTimeout(() => reject(new Error('CAPTCHA solve timeout')), 300000); // Delay set to 5min, consider of changing it
});
```

## Manual CAPTCHA Management

完全に制御したい場合は、挙動を設定するか、解決を完全に無効化してください。

### Disable Automatic CAPTCHA Solving

```javascript
Captcha.setAutoSolve({  
  autoSolve: false // Disable CAPTCHA solving  
});
```

### Disable CAPTCHA Auto-Solve for Specific Types

```javascript
Captcha.setAutoSolve({  
  autoSolve: true,  
  options: [{  
    type: 'usercaptcha', // Disable auto-solving for this CAPTCHA type  
    disabled: true  
  }]  
});
```

### Manually Solve CAPTCHAs

```javascript
(async () => {
  const page = await browser.newPage();
  const client = await page.target().createCDPSession();
  await client.send('Captcha.setAutoSolve', { autoSolve: false });
  await page.goto('https://site-with-captcha.com');
  try {
    const { status } = await client.send('Captcha.solve', { detectTimeout: 30000 });
    console.log('CAPTCHA solve status:', status);
  } catch (error) {
    console.error('Error solving CAPTCHA:', error);
  }
})();
```

## Supported CAPTCHA Types  

当社のソルバーは、以下を含む幅広い CAPTCHA をサポートしています:  

## Supported CAPTCHA Types  

当社のソルバーは、以下を含む幅広い CAPTCHA をサポートしています:  

- [**reCAPTCHA**](https://brightdata.jp/products/web-unlocker/captcha-solver/recaptcha)
- [**Click Captcha**](https://brightdata.jp/products/web-unlocker/captcha-solver/click-captcha)
- [**hCaptcha**](https://brightdata.jp/products/web-unlocker/captcha-solver/hcaptcha)
- [**PerimeterX**](https://brightdata.jp/products/web-unlocker/captcha-solver/perimeterx)
- [**SimpleCaptcha**](https://brightdata.jp/products/web-unlocker/captcha-solver/simplecaptcha)
- [**FunCaptcha**](https://brightdata.jp/products/web-unlocker/captcha-solver/funcaptcha)
- [**Cloudflare Turnstile**](https://brightdata.jp/products/web-unlocker/captcha-solver/cloudflare-turnstile)
- [**AWS WAF Captcha**](https://brightdata.jp/products/web-unlocker/captcha-solver/aws-waf-captcha)
- [**GeeTest CAPTCHA**](https://brightdata.jp/products/web-unlocker/captcha-solver/geetest-captcha)
- [**KeyCAPTCHA**](https://brightdata.jp/products/web-unlocker/captcha-solver/keycaptcha)
- [**Puzzle CAPTCHA**](https://brightdata.jp/products/web-unlocker/captcha-solver/puzzle-captcha)
- [**Yandex CAPTCHA**](https://brightdata.jp/products/web-unlocker/captcha-solver/yandex-captcha)
- [**Image CAPTCHA**](https://brightdata.jp/products/web-unlocker/captcha-solver/image-captcha)
- [**Text CAPTCHA**](https://brightdata.jp/products/web-unlocker/captcha-solver/text-captcha)

  

## Advanced Customization  

高度な設定を使用して、CAPTCHA 解決ロジックを微調整できます。  

### Example: Custom Options for Cloudflare Challenges  

```javascript
const cfOptions = {
  timeout: 40000,
  selector: '#challenge-body-text, .challenge-form',
  check_timeout: 300,
  success_selector: '#challenge-success[style*=inline]',
  wait_networkidle: { timeout: 500 }
};
```

## Pricing  

| **Plan**          | **Price (1K Results)** | **Monthly Cost** | **Description**                                                                   |  
|--------------------|------------------------|------------------|-----------------------------------------------------------------------------------|  
| **Pay-as-you-go**  | $1.50                 | No commitment    | アドホックなスクレイピングニーズに最適です。                                                 |  
| **Growth**         | $1.27                 | $499             | スケーリングするチーム向けに最適化されています。                                                       |  
| **Business**       | $1.12                 | $999             | 大規模なスクレイピング運用に適しています。                                     |  
| **Premium**        | $1.05                 | $1,999           | ミッションクリティカルな運用向けに、優先サポート付きの高度な機能を提供します。         |  
| **Enterprise**     | Custom Quote          | Contact Us       | カスタムパッケージ、プレミアム SLA、専任 Account Manager、SSO、およびパーソナライズされたソリューション。 |  

🚀 **SPECIAL OFFER**: 初回入金額と同額を、最大 **$500** まで付与します！  


## Why Developers Love CAPTCHA Solver  

- **簡単な統合**: Puppeteer、Playwright、Selenium とシームレスに動作します。  
- **高度な AI ベースのロジック**: リトライ、CAPTCHA 解決、フィンガープリンティング、IP ローテーション、高度なヘッダーを自動的に処理します。  
- **ブラウザ内蔵**: JavaScript レンダリングのために外部ブラウザを管理する必要はありません。  
- **リアルタイムのインサイト**: ライブダッシュボードでネットワークパフォーマンスを監視できます。  
- **比類ないサポート**: 24/7 のグローバルカスタマーサポートがあり、新機能が毎日追加されます。  


## FAQ  

### **How Does CAPTCHA Solver Work?**  
CAPTCHA Solver は、高度な AI ベースのロジックを使用して CAPTCHA を検知・解析し、自動的に解決します。  

### **Can It Handle Multiple CAPTCHAs Simultaneously?**  
はい。本ソリューションはスケールして、複数の CAPTCHA タイプを同時に処理できます。  

### **What Happens If CAPTCHA Solving Fails?**  
自動的にリトライが試行されます。問題が解決しない場合は、24/7 サポートチームにお問い合わせいただき、トラブルシューティングを行ってください。  


**🌟 今日から始めて、CAPTCHA にさよならしましょう！**  

**[Start Free Trial](https://brightdata.jp/products/web-unlocker/captcha-solver)**