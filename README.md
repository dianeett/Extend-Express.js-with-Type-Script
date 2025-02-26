import fetch from "node-fetch";

// Define or import the necessary types
interface ResponseItemType {
    id: number;
    name: string;
}

interface WeatherQueryInterface {
    zipcode: string;
}

interface WeatherDetailType {
    zipcode: string;
    weather: string;
    temp: number;
}

const routeHello = (): string => "Hello World!";

const routeAPINames = async (): Promise<string> => {
    const url = "https://www.usemodernfullstack.dev/api/v1/users";
    let data: ResponseItemType[] = [];
    try {
        const response = await fetch(url);
        data = (await response.json()) as ResponseItemType[];
    } catch (err) {
        console.error("Error fetching API data:", err);
        return "Error fetching data";
    }
    
    return data
        .map((item) => `id: ${item.id}, name: ${item.name}`)
        .join("<br>");
};

const routeWeather = (query: WeatherQueryInterface): WeatherDetailType =>
    queryWeatherData(query);

const queryWeatherData = (query: WeatherQueryInterface): WeatherDetailType => {
    return {
        zipcode: query.zipcode,
        weather: "sunny",
        temp: 35
    };
};

export { routeHello, routeAPINames, routeWeather };
