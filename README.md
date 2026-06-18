{
    "success": false,
    "message": "\nInvalid `prisma.mosque.create()` invocation:\n\n{\n  data: {\n    name: \"Baitul Mukarram\",\n    address: \"Topkhana Road, Dhaka\",\n    region: \"Dhaka\",\n    latitude: 23.7275,\n    longitude: 90.4099,\n+   user: {\n+     create: UserCreateWithoutMosquesInput | UserUncheckedCreateWithoutMosquesInput,\n+     connectOrCreate: UserCreateOrConnectWithoutMosquesInput,\n+     connect: UserWhereUniqueInput\n+   }\n  }\n}\n\nArgument `user` is missing."
}
