// api/proxy.js
// Serverless function (Vercel) yang jadi perantara antara StarPDF (browser)
// dan api.kyzzz.xyz. Karena request ini jalan di server, bukan di browser,
// CORS tidak berlaku, dan API key aman tersimpan sebagai environment
// variable (tidak pernah dikirim ke browser pengguna).

export const config = {
  api: {
    bodyParser: false, // penting: kita teruskan body multipart apa adanya
  },
};

const ENDPOINTS = {
  remini: "https://api.kyzzz.xyz/api/tools/remini",
  removebg: "https://api.kyzzz.xyz/api/tools/removebg",
};

export default async function handler(req, res) {
  // Izinkan dipanggil dari domain manapun tempat StarPDF di-hosting
  res.setHeader("Access-Control-Allow-Origin", "*");
  res.setHeader("Access-Control-Allow-Methods", "POST, OPTIONS");
  res.setHeader("Access-Control-Allow-Headers", "Content-Type");

  if (req.method === "OPTIONS") {
    res.status(204).end();
    return;
  }

  if (req.method !== "POST") {
    res.status(405).json({ error: "Method not allowed" });
    return;
  }

  const tool = req.query.tool;
  const target = ENDPOINTS[tool];
  if (!target) {
    res.status(400).json({ error: "Parameter 'tool' tidak valid. Gunakan 'remini' atau 'removebg'." });
    return;
  }

  const apiKey = process.env.KYZZ_API_KEY;
  if (!apiKey) {
    res.status(500).json({ error: "KYZZ_API_KEY belum diatur di environment variable server." });
    return;
  }

  try {
    // Kumpulkan raw body (multipart/form-data) apa adanya, lalu teruskan
    const chunks = [];
    for await (const chunk of req) chunks.push(chunk);
    const body = Buffer.concat(chunks);

    const upstream = await fetch(target, {
      method: "POST",
      headers: {
        "content-type": req.headers["content-type"] || "",
        "apikey": apiKey,
        "x-api-key": apiKey,
        "Authorization": apiKey,
      },
      body,
    });

    const contentType = upstream.headers.get("content-type") || "application/octet-stream";
    const resultBuffer = Buffer.from(await upstream.arrayBuffer());

    res.status(upstream.status);
    res.setHeader("content-type", contentType);
    res.send(resultBuffer);
  } catch (err) {
    res.status(502).json({ error: "Gagal menghubungi API Kyzz: " + err.message });
  }
}