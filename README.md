const { name, address, region, latitude, longitude, imamName, muazzinName, imageUrl, fajrTime, zuhrTime, asrTime, maghribTime, ishaTime } = req.body;

const mosque = await prisma.mosque.create({
  data: { 
    name, address, region, latitude, longitude,
    imamName, muazzinName, imageUrl,
    fajrTime, zuhrTime, asrTime, maghribTime, ishaTime,
    user: { connect: { id: userId } }
  },
});
