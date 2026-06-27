export const getUpcomingEvents = async (req, res) => {
  try {
    const now = new Date();
    const events = await prisma.event.findMany({
      where: {
        eventDate: { gte: now },
        status: "upcoming"
      },
      orderBy: { eventDate: "asc" },
      take: 3,
      include: {
        mosque: { select: { name: true } }
      }
    });

    res.status(200).json({
      success: true,
      count: events.length,
      data: events,
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      message: error.message,
    });
  }
};


<div class="search-box">
  <input type="text" id="mosqueSearchInput" placeholder="Search by region or name (e.g. Dhaka, Baitul)">
  <button onclick="searchMosque()">Search</button>
</div>

async function searchMosque() {
  const query = document.getElementById("mosqueSearchInput").value;
  if (!query) { alert("Please enter a region or name!"); return; }

  const div = document.getElementById("mosqueResults");
  div.innerHTML = "<p>Searching...</p>";

  try {
    // Search both by region and name simultaneously
    const [regionRes, nameRes] = await Promise.all([
      fetch(`${API}/mosques/region/${query}`),
      fetch(`${API}/mosques/search/${query}`)
    ]);

    const regionData = await regionRes.json();
    const nameData = await nameRes.json();

    // Merge results and remove duplicates
    const allMosques = [...(regionData.data || []), ...(nameData.data || [])];
    const unique = allMosques.filter((m, index, self) =>
      index === self.findIndex(t => t.id === m.id)
    );

    displayMosques(unique, div);
  } catch (err) {
    div.innerHTML = "<p>Search failed.</p>";
  }
}
